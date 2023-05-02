---
title: react 生命周期
date: 2022-09-09
categories: react
---



| 装载                   | 更新                             | 卸载 |
| ---------------------- | -------------------------------- | ---- |
| constructor            | setState \| props \| forceUpdate |      |
| getDrivedStateFromProps | getDrivedStateFromProps           |      |
| 											 | ShouldComponentUpdate           |      |
| render                 | render                           |      |
| 											 | getSnapshotBeforeUpdate			|      |
| React 更新真实Dom和Refs | React 更新真实Dom和Refs | componentWillUnMount     |
| ComponentDidMounted 	 | ComponentDidUpdate			|      |

![](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/20220926212434.png)

QA
1: 你好，"进入提交阶段，React 会先执行 Effect 的清理函数，然后再次执行 Effect。"
没理解这里为啥要effect 的清理函数，然后执行Effect，很反直觉。是为了执行后产生符合预期的值吗？

A: useEffect的详细内容在后面第10节课会讲，到放在这节课有点超纲，不过在这里我可以先剧透一下。 这里之所以大家会认为反直觉，很大程度上是因为大家把componentDidMount 和 componentWillUnmount 这一对类组件的生命周期方法当作了参照物。如果这样看的话，仿佛是在说同一个组件的 componentWillUnmount 发生在了 componentDidMount 之前，不合逻辑，理应出错的。 我建议这里先暂时不要考虑类组件，直接用副作用这个概念来理解。useEffect为函数组件声明了副作用，在不加入第二个参数（依赖值数组）的前提下，每次组件渲染都会执行，即每次渲染都会产生新的副作用（包含新的闭包），并留到这次的提交阶段执行，当执行的返回值是一个函数的时候，这个函数就是这次副作用的清理函数。 如第N次渲染，就会在提交阶段执行第N次副作用，返回第N次副作用的清理函数；下次第N+1次渲染，会在提交阶段先执行第N次副作用的清理函数，然后才是执行第N+1次副作用，返回第N+1次的清理函数；以此类推。

Q: 父子组件的生命周期执行顺序。

附和！之前常见在vue2中经常会去理解父子组件的生命周期函数执行顺序。如created（父） - created（子）- mounted（子）- created（父）。对于react  created 代表render前，mounted 代表render后。所以react 生命周期的执行顺序为。

class 组件：mount

constructor（父） - render (父) - constructor（子） - render(子) - componentdidmounted（子）- ComponentDidMounted（父）

update

setState（父）- ShouldComponentUpdate（父）- render（父）- props（子）- ShouldComponentUpdate（子）- componentDidUpdate（子）- componentDidUpdate（父）

Function 组件 + hooks

对于hooks来说，其实没有强声明周期的概念，useEffect /useLayoutEffect 里可以模拟组件的 componentDidMounted （render后） 和 componentWillUnMount （卸载前）。但是又不太一样的是，每次effect 的副作用函数重新执行之前都会去执行以下销毁函数（cleanup function）。