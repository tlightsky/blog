---
title: "Go里循环中错误使用结构体中的引用"
date: 2020-03-13T15:27:00+08:00
draft: true
---


源于这篇文章：
[一行Golang代码引发的血案——全网最详细分析2020年3月Let’s Encrypt证书吊销事故](https://zhuanlan.zhihu.com/p/111639968)

### 对于循环变量的理解

```go
type element struct {
	ele string
}

func getList() []*string {
	originMap := []element{
		{"A"},
		{"B"},
		{"C"},
	}
	arr := []*string{}
	for _, v := range originMap {
		arr = append(arr, &v.ele)
	}
	return arr
}

func TestWrongReference(t *testing.T) {
	arr := getList()
	assert.Equal(t, "C", *arr[0])
	assert.Equal(t, "C", *arr[1])
	assert.Equal(t, "C", *arr[2])
}

```

之类可以这么理解：
> * 变量的声明是在循环外面的，所以一直是一样的
> * 变量的内容是从slice里copy出来的，所以每次loop会变
> * 存在arr里的是这个变量内部的地址

```
./wrongreference.go:15:3: moved to heap: v
./wrongreference.go:8:24: getList []element literal does not escape
./wrongreference.go:13:18: []*string literal escapes to heap
```

从逃逸分析里可以看出v确实逃逸了，
所以分配在堆上，
但是逃逸的v在循环外部，
所以只有一个逃了，每次循环在堆内赋值

![golang-wrong-reference-1](/2020/golang-wrong-reference-1.jpg)


### 一种解决办法

```golang
type element struct {
	ele string
}

func getList() []*string {
	originMap := []element{
		{"A"},
		{"B"},
		{"C"},
	}
	arr := []*string{}
	for _, v := range originMap {
		vv := v
		arr = append(arr, &vv.ele)
	}
	return arr
}

func TestWrongReference(t *testing.T) {
	arr := getList()
	assert.Equal(t, "A", *arr[0])
	assert.Equal(t, "B", *arr[1])
	assert.Equal(t, "C", *arr[2])
}

```
这里就是强制在堆上分配三次了

```
./wrongreference.go:15:3: moved to heap: vv
./wrongreference.go:8:24: getList []element literal does not escape
./wrongreference.go:13:18: []*string literal escapes to heap
```

![golang-wrong-reference-2](/2020/golang-wrong-reference-2.jpg)
