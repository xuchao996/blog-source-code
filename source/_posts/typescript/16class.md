### Normal Usage

```ts
class Greeter1 {
  name: string; // init type
  constructor(otherName: string) {
    // receive init props value
    this.name = otherName;
  }
}
```

> for name,  the type annotation is optional, but will be an implicit `any` if not specified.



### strictPropertyInitialization(tsconfig.json)

> whether 

``` ts
// strictPropertyInitialization = true
class Greeter {
  name: string = 'foo'; // ok
}

class Greeter {
  name: string; 
  // ^__ error [ts] 属性“name”没有初始化表达式，且未在构造函数中明确赋值。
}
```



### readonly

```ts
class Greeter {
  readonly name: string = "world";
 
  constructor(otherName?: string) {
    if (otherName !== undefined) {
      this.name = otherName; // support readonly value is changed in constructor function.
    }
  }
 
  err() {
    this.name = "not ok";
		// Cannot assign to 'name' because it is a read-only property.
  }
}
```



### Constructor

- 和函数一样（支持parameter type 注释和 optional parameters 和 parameters default value）
- 支持重载

#### difference with function signature

- Constructor 不支持 type parameter - 整个放在 class 上

- Constructor 不支持 returns type annotations - 构造函数本身返回的类型即 class 本身




```ts
class Greeter3<T> {
  name: string = "foo";
  constructor(a: T, b: string) {}
  // constructor Greeter3<T>(a: T, b: string): Greeter3<T>
}

const greeter3 = new Greeter3("foo", "bar");
```

  

#### Super Calls

> when class extends  base class , super must be called in constructor function .



#### Accessors

##### get/set

```ts
class C {
  _length = 0;
  get length() {
    return this._length;
  }
  set length(value) {
    this._length = value;
  }
}
```

- 只有 get，没有 set 时 length 会变为 readonly 
- **type inference**: get accessors returns type can infer to set parameter type, 当没有添加set 参数类型的时候。
- Member Visibility

#### index Signature

```ts
class MyClass {
  [s: string]: boolean | ((s: string) => boolean);
 
  check(s: string) {
    return this[s] as boolean;
  }
}
```

**`as boolean` index signature type needs to also capture the types of methods.**

> Because the index signature type needs to also capture the types of methods, it’s not easy to usefully use these types. Generally it’s better to store indexed data in another place instead of on the class instance itself.



### implements（实现）

- class 可以 implements interface
- class 也可以 implements class
- implements 不同于 extends，需要声明所有的useable properties，extends 则不需要。



### Extends（继承）

- class extends class
- interface extends interface



##### Override methods

> 派生类 (Derived class) override的方法仍需要兼容其基类。

```ts
class Base2 {
    greet() {
        console.log("Hello, world!");
    }
}

class Derived2 extends Base2 {
    greet(name?: string) {
        if (name === undefined) {
            super.greet();
        } else {
            console.log(`Hello, ${name.toUpperCase()}`);
        }
    }
}
const dd = new Derived2();
dd.greet();
dd.greet("reader");
```

**Super Calls**

> 通过super去调用基类的field method



##### declare 

只做声明，不做初始化赋值，使用 declare



##### 派生类的执行顺序





##### 声明构造函数接口

```ts
interface Person {
  name: string;
  
}
```



### Member Visibility

#### public

#### protected

#### private

-  Can't access from outside the class

- Cant access from subclass properties

##### 一些缺陷

  ##### Cross-instance `private` access

##### private protect 仅可在TypeScript，但在 编译后的JavaScript 仍然可以访问。

##### 新的 ES 语法：JS通过 # 来保证私有。



### Static Member

> 挂在class上，而不是实例



- 可以和member visibility 一起使用

```ts
class S {
    private static b = 0;
}
S.b
// ^__ error 私有属性不可使用
````

  

- 一些key 不能作为属性名；例如：name length call

```ts
class S {
  static name = "S!";
  // ^__ error
}
```

##### 不能和*泛型*一起使用。

### this

> This 取决于运行时runtime.
>
> 多用于子类, other object.

#### this as parameter

```ts
// ts
class ClassA {
    fieldA = 0;
    doSomething(this: ClassA) {
        console.log(this.fieldA);
    }
}

const aa = new ClassA();

aa.doSomething(); // ok, no need arguments
```

```js
// js
class ClassA {
    fieldA = 0;
    doSomething() {
        console.log(this.fieldA);
    }
}
const aa = new ClassA();
aa.doSomething();
```

**ts 规避 this 问题**


```ts
class ClassA {
    fieldA = 0;
    doSomething(this: ClassA) {
        console.log(this.fieldA);
    }
}
class DerivedClassA extends ClassA {
}
const aa = new DerivedClassA();
const doSmt = aa.doSomething;
doSmt(); // [ts] 类型为“void”的 "this" 上下文不能分配给类型为“ClassA”的方法的 "this"
```



#### this as type

> This 也可以作为 type 使用。

**constructor parameter turn into properties**

> 通过在构造函数中声明的参数和type，可以被class 的实例继承。

```ts
class Pencil {
    constructor(readonly name: string, public width: number, private height: number) {

    }
}

const miniP = new Pencil('gangb', 10, 10);

miniP.name
miniP.width
miniP.height // [ts] 属性“height”为私有属性，只能在类“Pencil”中访问。
```

