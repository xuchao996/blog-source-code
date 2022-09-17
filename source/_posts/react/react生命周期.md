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


QA
1: 你好，"进入提交阶段，React 会先执行 Effect 的清理函数，然后再次执行 Effect。"
没理解这里为啥要effect 的清理函数，然后执行Effect，很反直觉。是为了执行后产生符合预期的值吗？

Q: 父子组件的生命周期执行顺序。

附和！之前常见在vue2中经常会去理解父子组件的生命周期函数执行顺序。如created（父） - created（子）- mounted（子）- created（父）。对于react  created 代表render前，mounted 代表render后。所以react 生命周期的执行顺序为。

class 组件：mount

constructor（父） - render (父) - constructor（子） - render(子) - componentdidmounted（子）- ComponentDidMounted（父）

update

setState（父）- ShouldComponentUpdate（父）- render（父）- props（子）- ShouldComponentUpdate（子）- componentDidUpdate（子）- componentDidUpdate（父）