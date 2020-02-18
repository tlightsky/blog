---
title: "Redux Sagas"
date: 2020-02-17T18:04:09+08:00
draft: false
---

### sagas背景
> * Sagas are Long Lived Transactions
> * Sagas are a lot of small transactions
> * Sagas are a Failure Management Pattern

[相关论文](http://www.cs.cornell.edu/andru/cs711/2002fa/reading/sagas.pdf)


### redux-sagas是专门用来处理副作用的，这样redux及react的其他部分就可以保持pure的状态
栗子：
```javascript
import { delay } from 'redux-saga'
import { put, takeEvery } from 'redux-saga/effects'

// ...

// Our worker Saga: 将执行异步的 increment 任务
export function* incrementAsync() {
  yield delay(1000)
  yield put({ type: 'INCREMENT' })
}

// Our watcher Saga: 在每个 INCREMENT_ASYNC action spawn 一个新的 incrementAsync 任务
export function* watchIncrementAsync() {
  yield takeEvery('INCREMENT_ASYNC', incrementAsync)
}
```

sagas使用`generator`而不是`await`来等待异步函数，

因为这样可以给调用方机会去`cancel`掉后续的执行，
每一个`yield`都是一个中断的机会

### takeEvery做了什么
查看[这里](https://github.com/redux-saga/redux-saga/blob/master/packages/core/src/internal/io-helpers.js#L18)
我们知道它`fork`了一个`worker`
```javascript
export function takeEvery(patternOrChannel, worker, ...args) {
  if (process.env.NODE_ENV !== 'production') {
    validateTakeEffect(takeEvery, patternOrChannel, worker)
  }

  return fork(takeEveryHelper, patternOrChannel, worker, ...args)
}
```

`sagas`内建了一个[状态机](https://github.com/redux-saga/redux-saga/blob/master/packages/core/src/internal/sagaHelpers/takeEvery.js#L11)，
用来持续执行`take` `fork`这两个动作
```javascript
  return fsmIterator(
    {
      q1() {
        return { nextState: 'q2', effect: yTake, stateUpdater: setAction }
      },
      q2() {
        return { nextState: 'q1', effect: yFork(action) }
      },
    },
    'q1',
    `takeEvery(${safeName(patternOrChannel)}, ${worker.name})`,
  )
```
这个地方有点类似于尾递归优化的[Trampoline](https://en.wikipedia.org/wiki/Trampoline_(computing))，

将递归转换成了状态机进行管理，
> * `take` 生成匹配的声明
> * `yFork` 生成执行`generator`的声明


### call, apply from sagas

```javascript
import { call } from 'redux-saga/effects'

function* fetchProducts() {
  const products = yield call(Api.fetch, '/products')
  // ...
}
```

```javascript
function* fetchProducts() {
  const products = yield apply(Api, Api.fetch, ['/products'])
  // ...
}
```

```javascript
import { cps } from 'redux-saga'

const content = yield cps(readFile, '/path/to/file')
```
这几个都是生命式调用，让`sagas`在`middleware`中进行调用，
方便进行测试

### put
类似call，但是是用来声明式`dispatch` `action`的
