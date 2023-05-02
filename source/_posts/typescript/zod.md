---
title: Zod 解决的是runtime type question
date: 2023-04-22
---



> 众所周知，Typescript 解决的是编码时的类型安全问题。但是对于运行时是没有解决的。而 Zod 是针对于*Runtime*的。



# Zod的使用

> Zod basic usage

## primitives (string, number, boolean, undefind)

```typescript
import {z} from "Zod";
const stringParser = z.string();
stringParser.parse(123) // throw error
```



## objects



### create a object schema

```typescript
import {z} from "Zod";
const PersonSchema = z.object({name: z.string()});

const getNameByData = (data) => {
	const parsedData = PersonSchema.parse(data); // 如果数据结构不支持，那么会抛错
  return parsedData.name;
}
```



### create a array schema

```ts
import {z} from "Zod";
const PersonSchema = z.object({name: z.string()});
const PersonListSchema = z.array(PersonSchema);

const getNameByDataList = (list) => {
	const parsedList = PersonSchema.parse(list); // 如果数据结构不支持，那么会抛错
  return parsedList[0].name;
}
```



### translate a typescript type from Zod

```typescript
import {z} from "Zod";
type PersonListType = z.infer(PersonListSchema);
// PersonListType = {name: string}[];
```



## other Type

**Zod** 通过组合各种function的方式，实现了联合类型。

### union types

```typescript
const Form = z.object({
  repoName: z.string(),
  privacyLevel: z.union([z.literal("private"), z.literal("public")]),
});
// mock type privacyLevel = "private" | "public";
```


```typescript
const stringOrNumber = z.union([z.string(), z.number()]);
// mock type stringOrNumber = string | number;
```


### optional 

```typescript
const Form = z.object({
  name: z.string(),
  phoneNumber: z.string().optional(),
  email: z.string(),
  website: z.string().optional(),
});
```


# Key
## 表单验证
> 做了运行时的Type 校验，表单验证感觉也是顺手为止。**Zod** 通过函数的方式接入了表单校验。



```typescript
import { z } from 'zod';

const Form = z.object({
  name: z.string(),
  phoneNumber: z.string().min(5).max(20).optional(), // 允许最大最小长度
  email: z.string().email(), // email 校验
  website: z.string().url().optional(), // 网站url 校验
});
```



还有很多扩展的方法，具体可以参考[文档](https://zod.dev/?id=strings)。
