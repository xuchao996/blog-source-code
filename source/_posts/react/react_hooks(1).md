1. 什么是 hooks？
2. 函数组件 + hooks 可以替代 class 吗？
3. 还有必要学习类组件吗？
4. react hooks 有哪些？

### 什么是 hooks？

Hook 直译是钩子的意思。在多种编程语言中都有这种概念。可以理解为钩子上挂了一段代码。
在 React 中，Hooks 组织了 React FC（react Function Component） 的代码逻辑。
用来实现代码的副作用。
这里提到了**副作用**，一般在纯函数（Pure Function）中，其实会讨厌这个概念。因为它（纯函数）的存在，导致了函数不是一个纯粹的函数。

> 当一个函数满足如下条件时，就可以被认为是纯函数：
>
> 函数无论被调用多少次，只要参数相同，返回值就一定相同，这一过程不受外部状态或者 IO 操作的影响；
>
> 函数被调用时不会产生副作用（Side Effect），即不会修改传入的引用参数，不会修改外部状态，不会触发 IO 操作，也不会调用其他会产生副作用的函数。

```javascript
function add(x, y) {
  return x + y;
}
```

上面的 add 方法同时满足上述两个条件，故是纯函数。

**hooks 的存在，即把一个函数变成一个不纯的函数。**
对于一个纯函数组件来说，它应该是这个样子。

```jsx

    function List(props) {
        return props.list.map(item => (
            <Item> {item} <Item>
        ))
    }

```

即只有外部状态去渲染当前的组件，并且相同的值渲染的结果是一致的。
对于一个简单的纯渲染关系来说，我们可以使用这种方式。但是，大部分的逻辑都是复杂的，需要状态及生命周期去管理维护。所以 hooks 就是解决这个事情。
从上述描述其实可以狭义的去理解为，hooks 就是函数的副作用。

> **Hooks 就是这样一套为函数组件设计的，用于访问 React 内部状态或执行副作用操作，以函数形式存在的 React API。**注意，这里提到的“React 内部状态”是比组件 state 更广义的统称，除了 state 外，还包括后面课程中会详细讲解的 context、memo、ref 等。

一个简单的例子

```jsx
// 一个状态 0 - 1 的例子
function ShowModifyItem(props) {
    const [status, setStatus] = useState(0);
    setTimeout(function() {
        setStatus(1);
    })
    return (
        <div>
            {<span>展示 { status }</span>}
        <div>
    )
}
```

### reactHooks 有哪些？

基础：

- useState
- useEffect
- useContext

延伸

- useReducer
- useMemo
- useCallback
- useRef
- useImperativeHandle
- useLayoutEffect
- useDebug
  ...

#### useState

hooks 里的状态钩子。

#### useReducer

hooks 里的状态钩子。

#### useRef

    - 存放 DOM 的引用
    - 存放一个可变值（可变值的概念是对应于react state 的不可变性）
    - 可变值/可变对象有一个 ** 可供读写的 current ** 属性，组件重新渲染本身不会影响 current 属性的值；反过来，变更 current 属性值也不会触发组件的重新渲染。
