|           |      |      |
| --------- | ---- | ---- |
| null      | js提供，ts继承了过来 | 非对象类型 |
| undefined |      |      |
| string    |      |      |
| number    |      |      |
| boolean    |      |      |
| bigint    |      |      |
| symbol    |      |      |
| object(Array Function Date，===) turple |  | 对象类型 |
| void   | ts 扩展 | ts扩展类型 |
| never    |      |      |
| enum    |      |      |
| unknown    |      |      |
| any    |      |      |
| type    | 关键字 |      |
| interface    | 关键字 |      |



理解 **TS** 类型

js里的类型和值

而ts只有类型，没有值。



包装对象

包装和拆包

```js
const a = 123;
a.toFixed(2); // '123.00'
// a作为number类型为啥会有toFixed 的方法，这是因为其引擎内部做了装箱和拆箱的操作
temp = new Number(123);
curr = temp.toFixed(2)
temp = null;
return curr;
```



非对象类型可以直接使用。

对象类型分类

​	[Array](./6索引签名.md)（不直接用，一般用在定义泛型上）

​	[Object](./6索引签名.md)（一般不用，不够精确）

​	Function （一般不用，不够精确）

​	...其他类型基本可使用



**包装类型**（number，string，boolean）

```ty
01  let a : boolean = new Boolean(1) ;  //错误
02  let b : boolean = Boolean(1) ;      //正确
```

在TypeScript中，Number、String和Boolean分别是number、string和boolean的封装对象。



**number**

JS/TS 只有一种类型去表示数值。就是**number**。

整数（10进制数） 100

浮点数 

```
let fl = 12.001;
```

2进制数

```js
let x2 = 0b10110;
```

8进制数

```js
let x8 = 0o744;
```

16进制数

```js
let x16 = 0x111b;
```



正是因为没有区分多种数字类型，所以一般牵扯到小数计算会产生精度丢失问题。转为**整数**类型可解。

**string（字符串）**

一般用单引号或者双引号包裹的字符可以声明为字符串，js/ts 里只有字符串。还可以用模板字符串去表示（模板字符串是ECMAScript 6 之后提供的表示字符串的能力）。

**boolean**

一般只包含2个值（false， true），表示条件的结果，非正即假。



[**enum（枚举）**](./10枚举.md)



**never** 

所有类型（包括null, undefined）的子类型，所以可以赋值给任何类型。



**[any 与 unknown](./9any和unknown的区别.md)**



**symbol**



**交叉类型**&

> 将多个类型合为一个类型。可以使用每个类型的独有类型。



**Union 类型 |**

> Union 后的类型，不确定是哪一个类型的时候，只能使用其共有类型，使用独有类型会报错。

```ts
```



**类型别名**

> 用来给对象类型和联合类型命名
>
> 理解为变量表达式的命名；

```
type A = {[string] : "a" | "b" | "c"}
interface A {
	[k: string]: "a" | "b" | "c";
}
```

与interface的区别：

- type A 的类型 是 *"a" | "b" | "c"* ，interface A 的类型真的是A。

[handbook关于两者区别的描述](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)



- **interface 可以重复赋值**

例如在给全局变量Window 添加属性声明时；window是lib.d.ts上声明的文件，但是有时需要挂一些自定义的变量，不然ts会报错。

```ts
declare interface Window {
  getParam: { [k: string]: any }
  webkit: { [k: string]: any }
}
```





#### [类型断言](./11断言.md)



**数组与元组**

元组是数组的一个子集，一般是一个规定长度规定每个元素类型的数据结构。

具有以下特点：

- 元组的数据类型可以是任何类型。　

- 在元组中，可以包含其他元组。　

- 元组可以是空元组。　

- 元组赋值必须元素类型兼容。　

- 元组的取值同数组的取值，元素的标号从0开始。　

- 元组可以作为参数传递给函数。

  

```ts
let tuple1: [number, string, boolean] = [1,'', false]; // tuple1 type => [number, string, boolean];

```

但如果依赖类型推导，那么会和预想的结果不一致。

```ts
let tuple2 = [1,'', false]; // tuple2 type => <stirng|number|boolean>Array

```

会是一个联合类型的数组类型。这是一个需要**注意**的点。



元组的获取元素与数组相同，都是通过下标进行访问。



元组的常见问题；

- 越界（越界会报错）

​	不能访问超过tuple.length的元素

​	元组解构超过tuple.length 

​	
