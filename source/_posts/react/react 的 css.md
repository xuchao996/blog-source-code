1. CSS Modules

```jsx
import s from "./Web.module.scss"; 
// 会把 css 编译成带一串hash 的class类名
import c from "classnames"; // 简化react 的class 连接方式
export const Web = () => {
  return (
  	<div className={s.wrapper}></div>
  )
}
```





2. styled Component

```jsx

```

   

3, unocss, tailwind, windcss

Css 原子化