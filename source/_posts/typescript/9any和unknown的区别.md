---
title: "any和unknown的区别"
date: "2022-08-08"
---

```ts
type any = string | number | object | boolean | 
```

Unknown 有一次类型断言的机会

```ts

type A = unknown
const a: A = 1
// a.toFixed(2) -- error
;(a as number).toFixed(2)

type B = any
const b: B = 1
b.toFixed(2)

```



any 则可以随意用。



-----------------



never 最小集合

```
type A = string & number;

```

会放在条件语句的补充类型，使用不到。