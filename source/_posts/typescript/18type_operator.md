---
title: type operator
---



### keyof 

> The `keyof` operator takes an object type and produces a string or numeric literal union of its keys. 



### typeof 

- refer to the *type* of a variable or property
- 结合 `ReturnType` 获取实际函数的返回值类型

```ts

function f(a: string, b:string) {
    return a + b;
}

type a11 = ReturnType<f> // error
type a11 = ReturnType<typeof f> // ok
```



### Indexed Access Types(索引访问类型)

- 获取**值**类型
- 获取数组内的值类型
- 结合 **keyof** 获取所有值类型

```ts
type Age = Person["age"];
type AgeAndName = Person["age" | "name"];
type All1 = Person[keyof Person];
```

- 也可以接收对象的keyof，获取对象值的类型
```ts
type a = {
  a: stirng;
  b: string;
  c: number;
}
type b = a[keyof a] // => string | number 
```



- 类型只能接收类型

### Indexed Union Types(索引联合类型)

```ts

type test3 = {
  key: 'cow'
  value: 'yellow'
  sun: false
}

type testExpect3 = {
  key: 'cow'
  value: 'yellow'
  sun: false
  isMotherRussia: false | undefined
}

type cases = [
  Expect<Equal<AppendToObject<test3, 'isMotherRussia', false | undefined>, testExpect3>>,
]

// ============= Your Code Here =============

type AppendToObject<T, U extends string, V> = {
  [K in keyof T | U]: K extends U ? V : K extends keyof T ? T[K] : never;
}
// merge 对象操作
```



### Conditional Type(条件类型)

类型编程 依赖 `extends` 作为条件，返回 `TrueType` or `FalseType`

`  SomeType extends OtherType ? TrueType : FalseType`  



> When the type on the left of the `extends` is assignable to the one on the right, then you’ll get the type in the first branch (the “**true**” branch); otherwise you’ll get the type in the latter branch (the “**false**” branch).



#### eg：递归平铺

```ts
type Flatten<T> = T extends any[] ? Flatten<T[number]> : T;
type Complex = [
    [
        [string]
    ]
]

type res1 = Flatten<number>; // number 
type res2 = Flatten<Complex>; // string
```



#### Inferring Within Conditional Types

eg：递归平铺使用infer

```ts
type Flatten<Type> = Type extends Array<infer Item> ? Flatten<Item> : Type;
type Complex = [
    [
        [string]
    ]
]

type res1 = Flatten<number>; // number
type res2 = Flatten<Complex>; // string
```

##### 通过关键字 infer 声明了一个新的类型变量，infer 可以作为中间值进行后续运算也可以作为结果。

- 可以作为函数签名返回值类型；例如 **ReturnType** utilsType
- 可以作为数组的元素类型；例如

##### 对于重载的函数签名是只能推断最后一个函数签名。



```ts
declare function stringOrNum(x: string): number;
declare function stringOrNum(x: number): string;
declare function stringOrNum(x: string | boolean): string | boolean;

type T1_1 = ReturnType<typeof stringOrNum>; // string | boolean
```



#### Distributive(分配律)

如果是在条件类型中使用**联合类型**，那么则符合分配律的结果。

**即联合类型的结果仍然是联合类型**

```ts
type ToArray<T> = T extends any ? T[] : never;
type _3 = ToArray<string | number>;
	// ^__  yes type _3 = string[] | number[] 
  // not string | number []

```



```
ToArray<string | number>
==>
ToArray<string> | ToArray<number>;
==>
string[] | number[]
```

##### never是特殊的联合类型

```ts
type ExA<T> = T extends string ? true : false;
type res = ExA<never>;
// type res = never

```



eg

- Exclude
- Extract
- Pick



##### how to fix the question

```ts
type ToArrayNonDist<Type> = [Type] extends [any] ? Type[] : never;
 
// 'StrArrOrNumArr' is no longer a union.
type StrArrOrNumArr = ToArrayNonDist<string | number>;
```



### Mapped Types

类似于[index signature](./6索引签名.md)，但可以做泛型化处理。



#### Mapping Modifiers

> 通过 “**+**” or “**-**” 添加或移除修饰符（readonly、 ?）

```ts
type K<T> = {
    [k in keyof T]-?: boolean;
  							//^__ 移除了可选修饰符
}

type FeatureFlags = {
    name?: string;
    darkMode: () => void;
    newUserProfile: () => void;
};

type FeatureK = K<FeatureFlags>;
/*
  type FeatureK = {
      name: boolean;
      darkMode: boolean;
      newUserProfile: boolean;
  }
*/

// if 
type K<T> = {
    [k in keyof T]+?: boolean;
}
// So
/*
  type FeatureK = {
      name?: boolean | undefined;
      darkMode?: boolean | undefined;
      newUserProfile?: boolean | undefined;
  }
*/

```



#### Key Remapping via *as*

> In TypeScript 4.1 and onwards, you can re-map keys in mapped types with an `as` clause in a mapped type

```TS
type removeOptional<T> = {
    [K in keyof T]-?: T[K];
}

type ConvertKeys<T> = {
    [K in keyof T as `get${Capitalize<K & string>}`]: T[K];
}
// ===>>>
type ConvertKeys<T> = {
    [K in keyof T as `get${Capitalize<K & string>}`]-?: T[K];
}

type _ = ConvertKeys<removeOptional<Person>>;
/*
type _ = {
    getName: string;
    getAge: number;
    getWeight: number;
}
*/
```



```ts

type SquareEvent = { kind: "square", x: number, y: number };
type CircleEvent = { kind: "circle", radius: number };

type EventConfig<T extends {kind: string}> = {
    [E in T as E["kind"]]: (k: E) => void;
}
/**
 * 
 type Config = {
     square: (event: SquareEvent) => void;
     circle: (event: CircleEvent) => void;
 }
 */
type Config = EventConfig<SquareEvent | CircleEvent>

```

#####  a mapped type using a conditional type 



### Template Literal Types

```ts
type World = 'world';

type Greeting = 'hello' + World; // error 没有二元运算

type Greeting = `hello ${World}` // type Greeting = "hello world"
```



#### use union type

```ts
type EmailLocaleIDs = "welcome_email" | "email_heading";
type EmailLocaleID = `${EmailLocaleIDs}_id`;
// ^__ type EmailLocaleID = "welcome_email_id" | "email_heading_id"

type FooterLocaleIDs = "footer_title" | "footer_sendoff";

type AllLocaleIDs = `${EmailLocaleIDs | FooterLocaleIDs}_id`;
// ^__ type AllLocaleIDs = "welcome_email_id" | "email_heading_id" | "footer_title_id" | "footer_sendoff_id"

```

**符合分配律知识**

