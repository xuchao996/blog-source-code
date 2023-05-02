---
title: react 疑问
---

1，react 为啥会有 **不可变性** 这个概念？

 rt，react 对于**数据/状态**的管理上出现了 immutable 这类的技术，在很多 react 生态 技术上也会出现相关概念，不明白这是为什么？

**对于 react 的两个变量 props 和 state**

**props** 是不能在内部组件修改

**state** 在 class 组件和 hooks 组件都是通过 setState 去修改的，不能直接修改。

在 hooks 中 存在**记忆化（memoried）**的概念。

useState 钩子具备记忆化。

import update from 'immutability-helper'

[Immutable 详解及 React 中实践](https://zhuanlan.zhihu.com/p/20295971)

**shallow equal**

FiberNode

首先不是普遍意义上的 parent-children 结构 而是 parent-child 的结构，他是一个链表结构。

Parent-child - child - sibling，即父子关系是单向的，通过 sibling 完成兄弟之前的链接。

”这棵树可以随时暂停并恢复渲染，

触发组件生命周期等副作用（Side-effect），

并将中间结果分散保存在每一个节点上，

不会 block 浏览器中的其他工作。“
这里引用了文档中描述，fiber 简要做了四件事情，但是好像都不太理解他是怎么操作的。



Reconciliation - (调和 / 协调)

