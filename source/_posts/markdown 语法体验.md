---
title: markdown 语法体验
date: 2022-08-01 11:42:42
tags: markdown
categories: other
---

### Emoji

:100:

:tada:

[Emoji](https://github.com/markdown-it/markdown-it-emoji/blob/master/lib/data/full.json)

[[toc]]

[[toc]]

[[toc]]

[[toc]]

::: tip

fdafdfsadfsdfsfd asf

### 标题

# 标题一

## 标题二

### 标题三

#### 标题四

##### 标题五

###### 标题六

### 代码块

```js
export const foo = {
  name: "foo",
  age: 18,
};
```

### 链接

#### 内联链接

[gogo](www.google.com)

#### 全局链接

[gogogog][gourl]

[gourl]: www.google.com

### 图片

多了一个感叹号(!)

![tiger](https://cdn.jsdelivr.net/gh/xuchao996/gallary@main/imgs/Tiger.50.jpg)

#### 全局图片

![Black cat][black]

![Orange cat][orange]

[black]: https://upload.wikimedia.org/wikipedia/commons/a/a3/81_INF_DIV_SSI.jpg
[orange]: http://icons.iconarchive.com/icons/google/noto-emoji-animals-nature/256/22221-cat-icon.png

### 引用块

> luis ren zou

#### 列表

- 1
  - 1.1
  - 1.2
- 2
  - 2.1
- 3
- 4

#### 段落

换行 （只有回车）

We pictured the meek mild creatures.
where They dwelt in their strawy pen,
Nor did it occur to one of us there
To doubt they were kneeling then.

换行（末尾通过两个空格）

We pictured the meek mild creatures where  
They dwelt in their strawy pen,  
Nor did it occur to one of us there  
To doubt they were kneeling then.

### Table

| Table header | Table header2 |
| ------------ | ------------- |
| pub          | pri           |
| pub2         | pri1          |
| pub2         | pri1          |
