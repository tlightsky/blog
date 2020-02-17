---
title: "React Hooks Concepts"
date: 2020-02-15T23:07:54+08:00
draft: false
---


### useEffect


```javascript
useEffect(
  () => {
    const subscription = props.source.subscribe();
    return () => {
      subscription.unsubscribe();
    };
  },
  [props.source],
);
```

主要函数同`componentDidMount` `componentDidUpdate`，
返回的函数同`componentDidUmount`，
由传入的`source`来决定是否触发

### useState

```javascript
const [state, setState] = useState(initialState);
```
按位置挂在状态，所以外层不要有分支，不要有循环，不然可能挂载出错

内容改变后会触发`render`

### useRef

同useState，但不触发`render`

```typescript jsx
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` 指向已挂载到 DOM 上的文本输入元素
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

通常也被用来这样引用`Dom`树

另外同`createRef`不同的点是，不会每次render都创建新的

### useContext

当前的 context 值由上层组件中距离当前组件最近的 <MyContext.Provider> 的 value prop 决定，
context可以被用来做主题切换。

`useContext`的优先级比祖先的`React.memo` `shouldComponentUpdate`高

```typescript jsx
const themes = {
  light: {
    foreground: "#000000",
    background: "#eeeeee"
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222"
  }
};

const ThemeContext = React.createContext(themes.light);

function App() {
  return (
    <ThemeContext.Provider value={themes.dark}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);

  return (
    <button style={{ background: theme.background, color: theme.foreground }}>
      I am styled by theme context!
    </button>
  );
}
```