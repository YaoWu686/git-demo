# TypeScript

## 概述

1. `TypeScript`包含了`JavaScript`的一切功能，并且在`JavaScript`的基础上引入了**类型系统**。故：<span style="color: #42b983; font-weight: bold;">JavaScript是TypeScript的子集，TypeScript是带有类型的JavaScript</span>

## tsc

`TypeScript`代码是无法直接执行的，它必须转化为`JavaScript`才能够执行

`tsc`工具是`TypeScript`的编译器，它能够将`TypeScript`代码编译为`JavaScript`代码， 从而执行`TypeScript`代码

- 全局安装

    `tsc`工具可以全局安装，安装完后在命令行中输入`tsc`命令即可使用

    首先，需要全局安装`typescript`：

    ```powershell
    npm i -g typescript
    ```

    安装完后，测试`tsc`的版本号：

    ```powershell
    tsc --version
    ```

    可以看到版本信息的话，说明`tsc`工具全局安装就完成了

- 本地安装

    当然，`tsc`工具也可以在项目中进行安装

    假设在当前目录中创建一个项目`test`，下面对其进行创建，并初始化：

    ```powershell
    md test
    cd test
    npm init -y
    ```

    这时，在项目本地安装`typescript`，这里将其安装为“**开发依赖**”：

    ```powershell
    npm i -D typescript
    ```

    这时，想要使用`tsc`工具，就需要使用`npx`，下面查看`tsc`工具的版本信息：

    ```powershell
    npx tsc --version
    ```

## 类型注解

### 变量类型注解

1. 可以显式地指定变量的类型

    ```typescript
    let name: string;				// 显式指定变量name的类型为string
    let gender: string = '男';	   // 显式指定变量gender的类型为string
    ```

2. 变量存在初始化表达式时，可以省略变量类型，编译器会自动推断类型

    ```typescript
    let name = '小明';		// 省略类型，自动推断类型为string
    let age = 18;			 // 省略类型，自动推断类型为number
    ```

### 函数类型注解

可以为函数指定参数类型和返回值类型

```typescript
function func(x1: number, x2: number): void {
    // 同时指定了参数类型和返回值类型
}
```

当函数是匿名函数时，并且通常是函数作为回调函数使用时，匿名函数不需要指定参数类型和返回值类型

```typescript
const names: string[] = ['Alice', 'Bob', 'Eve'];

names.forEach((e) => {
    // xxx 				回调函数无需指定类型
});
```

### 数组类型注解

### 元组类型注解

### 对象类型注解

```typescript
function printName(obj: { first: string; last?: string; }) {
    // 这里参数obj的类型为对象类型
}
```

**可选参数**：上述例子中对参数obj的类型说明中，last属性就是一个可选属性







# 官网笔记摘要

- *Static types systems* describe the shapes and behaviors of what our values will be when we run our programs. 

    > TypeScript的静态类型系统只是描述了值的形状和行为（长什么样子，有哪些东西）

- For example, the specification says that trying to call something that isn’t callable should throw an error. Maybe that sounds like “obvious behavior”, but you could imagine that **accessing a property that doesn’t exist on an object** should throw an error too. Instead, JavaScript gives us different behavior and returns the value `undefined`

    > 在JavaScript中，访问对象身上不存在的属性时，返回`undefined`，但是在TypeScript中，会**报错**

- Keep in mind, we don’t always have to write explicit type annotations. In many cases, TypeScript can even just *infer* (or “figure out”) the types for us even if we omit them.

    > 很多时候，我们不需要显式声明变量类型，TypeScript会进行自动类型推导

    The type of a variable is inferred based on the type of its initializer

    > 变量类型的推导基于其右侧的初始化表达式

- it’s best not to add annotations when the type system would end up inferring the same type anyway.

    > TypeScript能进行类型推断时，最好不要手动添加类型注解

- Type annotations aren’t part of JavaScript (or ECMAScript to be pedantic), so there really aren’t any browsers or other runtimes that can just run TypeScript unmodified. That’s why TypeScript needs a compiler in the first place - it needs some way to strip out or transform any TypeScript-specific code so that you can run it. Most TypeScript-specific code gets erased away, and likewise, here our type annotations were completely erased.

    > TypeScript在转化为JavaScript时，会**擦除**所有的类型注解（Erased Types）

- TypeScript has the ability to rewrite code from newer versions of ECMAScript to older ones such as ECMAScript 3 or ECMAScript 5 (a.k.a. ES5). This process of moving from a newer or “higher” version of ECMAScript down to an older or “lower” one is sometimes called *downleveling*.

    > TypeScript代码在转化为JavaScript代码时，可以进行兼容性处理，将高版本的语法转化为低版本的等效语法（Downleveling）

- By default, values like `null` and `undefined` are assignable to any other type.

    > 默认情况下，`null`和`undefined`可以为其他任何类型的变量赋值（这并不好，可以通过开启`strictNullChecks`开关来解决）

- TypeScript also has a special type, `any`, that you can use whenever you don’t want a particular value to cause typechecking errors.

    When a value is of type `any`, you can access any properties of it (which will in turn be of type `any`), call it like a function, assign it to (or from) a value of any type, or pretty much anything else that’s syntactically legal.

    Using `any` disables all further type checking, and it is assumed you know the environment better than TypeScript.

    > TypeScript中，类型`any`可以用于跳过语法检查

- When you don’t specify a type, and TypeScript can’t infer it from context, the compiler will typically default to `any`.

    > 当没有指定类型，TypeScript编译器也没法推断出类型时，默认类型为`any`

    You usually want to avoid this, though, because `any` isn’t type-checked. Use the compiler flag [`noImplicitAny`](https://www.typescriptlang.org/tsconfig#noImplicitAny) to flag any implicit `any` as an error.

    > 启动`noImplictANy`后，任何隐式的`any`类型都会导致错误

- If you want to annotate the return type of a function which returns a promise, you should use the `Promise` type:

    ```typescript
    async function getFavoriteNumber(): Promise<number> {
      return 26;
    }
    ```

- When a function appears in a place where TypeScript can determine how it’s going to be called, the parameters of that function are automatically given types.

    ```typescript
    const names = ["Alice", "Bob", "Eve"];
    
    names.forEach((s) => {			// 这里的参数s能够自动推导出类型为string
      console.log(s.toUpperCase());
    });
    ```

    > 函数作为参数传递给另一个函数时，往往这个函数的形参类型都能够被隐式推导（因为在另一个函数的参数中进行了声明）（***Contextual Typing***，上下文类型推导）

- A union type is a type formed from two or more other types, representing values that may be *any one* of those types.

    > 联合类型（***Union Types***）

- TypeScript will only allow an operation if it is valid for *every* member of the union. For example, if you have the union `string | number`, you can’t use methods that are only available on `string`

    > 联合类型的变量只能使用所有类型公共的方法和属性
    >
    > 
    >
    > 可以使用**类型窄化**（***Narrowing***）一步一步的将联合类型窄化为更加具体的类型

    ```typescript
    function printId(id: number | string) {
      if (typeof id === "string") {
        // 在这个分支里，id的类型为string
        console.log(id.toUpperCase());
      } else {
        // 这个分支里，id的类型为number
        console.log(id);
      }
    }
    ```

- Being concerned only with the structure and capabilities of types is why we call TypeScript a *structurally typed* type system.

    > 只关注类型的[结构](#)和[功能](#)，这就是为什么我们称 TypeScript 为一个基于结构类型的类型系统

- Sometimes you will have information about the type of a value that TypeScript can’t know about.

    For example, if you’re using `document.getElementById`, TypeScript only knows that this will return *some* kind of `HTMLElement`, but you might know that your page will always have an `HTMLCanvasElement` with a given ID.

    In this situation, you can use a *type assertion* to specify a more specific type:

    ```typescript
    const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
    ```

    > 类型断言（***Type Assertions***）

- TypeScript only allows type assertions which convert to a *more specific* or *less specific* version of a type. This rule prevents “impossible” coercions like:

    ```typescript
    const x = "hello" as number;
    ```

    > 类型断言不是乱搞！！！

- Sometimes this rule can be too conservative and will disallow more complex coercions that might be valid. If this happens, you can use two assertions, first to `any` (or `unknown`, which we’ll introduce later), then to the desired type:

    ```typescript
    const a = expr as any as T;
    ```

    > 类型断言有时候也能乱搞！**如果你真的需要的话**！！！

- The `as const` suffix acts like `const` but for the type system, ensuring that all properties are assigned the literal type instead of a more general version like `string` or `number`.

    ```typescript
    const req = { url: "https://example.com", method: "GET" } as const;
    ```

    > `as const`后缀

- TypeScript also has a special syntax for removing `null` and `undefined` from a type without doing any explicit checking. Writing `!` after any expression is effectively a type assertion that the value isn’t `null` or `undefined`:

    ```typescript
    function liveDangerously(x?: number | null) {
      // No error
      console.log(x!.toFixed());
    }
    ```

    Just like other type assertions, this doesn’t change the runtime behavior of your code, so it’s important to only use `!` when you know that the value *can’t* be `null` or `undefined`.

    > **非空断言**（***Non-null Assertion***）

# 类型守卫（Type Guards）

- `typeof`（typeof守卫）

    支持的类别：

    - `typeof value === 'string'`
    - `typeof value === 'number'`
    - `typeof value === 'boolean'`
    - `typeof value === 'bigint'`
    - `typeof value === 'symbol'`
    - `typeof value === 'undefined'`
    - `typeof value === 'object'`
    - `typeof value === 'function'`

- `Truthiness Checking`（真值检查）

    ```typescript
    function printAll(strs: string | string[] | null) {
        if (strs && typeof strs === 'object') {
            // 这个分支时，strs的类型为string[]
            // 这种通过判断布尔值的方式来窄化类型的方式就是`真值检查`
            for (const s of strs) {
                console.log(s);
            }
        } else if (typeof strs === 'string') {
            // 这个分支时，strs的类型为string
            console.log(strs);
        } else {
            // 这个分支时，strs的类型为null
            console.log('null');
        }
    }
    ```

- `Equality`（相等性检查）

    TypeScript also uses `switch` statements and equality checks like `===`, `!==`, `==`, and `!=` to narrow types.

- `in`（`in`操作符）

    JavaScript has an operator for determining if an object or its prototype chain has a property with a name: the `in` operator. TypeScript takes this into account as a way to narrow down potential types.

- `instanceof`（`instanceof`操作符）

    ```typescript
    function logValue(content: Date | string): void {
        if (content instanceof Date) {
            // content的类型为Date
            console.log(content.toUTCString());
        } else {
            // content的类型为string
            console.log(content.toUpperCase());
        }
    }
    ```

- `Control flow analysis`（控制流分析）

    ```typescript
    function padLeft(padding: number | string, input: string) {
        if (typeof padding === 'nubmer') {
            return ' '.repeat(padding) + input;
        }
        // 上面if语句所在的分支中，padding的类型被窄化为number了，并且
        // 如果执行了上述的if语句，那么就不可能会到达这里的return语句，
        // 因此，下面的语句但凡能执行，都说明padding的类型不可能为number,
        // 因此，到达这里时，padding的类型被窄化为了string
    
        // 这种就是基于`控制流`的类型窄化
        return padding + input;
    }
    ```

- `type predicates`（类型谓语）（自定义的类型窄化方式、自定义的类型守卫）

    To define a user-defined type guard, we simply need to define a function whose return type is a *type predicate*:

     A predicate takes the form `parameterName is Type`, where `parameterName` must be the name of a parameter from the current function signature.

    ```typescript
    function isFish(pet: Fish | Bird): pet is Fish {
        return (pet as Fish).swim !== undefined;
    }
    ```

- `Assertion functions`

- `discriminated union`（可辨识联合）

     When every type in a union contains a common property with literal types, TypeScript considers that to be a *discriminated union*, and can narrow out the members of the union.

    ```typescript
    interface Circle {
        kind: 'circle';
        radius: number;
    }
    
    interface Square {
        kind: 'square';
        sideLength: number;
    }
    
    type Shape = Circle | Square;
    
    function getArea(shape: Shape) {
        if (shape.kind === 'circle') {
            // 此时，shape的类型被窄化为Circle
            return Math.PI * shape.radius ** 2;
        }  else {
            // 此时，shape的类型被窄化为Square
            return shape.sideLength ** 2;
        }
    }
    ```

- `Exhaustiveness checking`（穷尽性检查）

    The `never` type is assignable to every type; however, no type is assignable to `never` (except `never` itself).

    This means you can use narrowing and rely on `never` turning up to do exhaustive checking.

    ```typescript
    interface Circle {
        kind: 'circle';
        radius: number;
    }
    
    interface Square {
        kind: 'square';
        sideLength: number;
    }
    
    type Shape = Circle | Square;
    
    function getArea(shape: Shape) {
        if (shape.kind === 'circle') {
            // 此时，shape的类型被窄化为Circle
            return Math.PI * shape.radius ** 2;
        }  else if (shape.kind === 'square'){
            // 此时，shape的类型被窄化为Square
            return shape.sideLength ** 2;
        } else {
            // 此时，所有的可能已经穷尽了，因此shape的类型为never
            // 这时，下面的语句不会报错，说明已经穷尽了
            let value: never = shape;
            
            // 如果上面的语句报错的话，说明shape的类型必定不为never，
            // 也就说明类型还没有被穷尽
        }
    }
    ```


# 函数类型

- `Function Type Expressions`

    The simplest way to describe a function is with a *function type expression*. These types are syntactically similar to arrow functions:

    ```typescript
    function doSomething(fn: (a:string)=>void) {
        // 这里的函数形参 fn 的类型声明就使用了函数类型表达式
        fn('Hello World');
    }
    
    function printToConsole(value: string): void {
        console.log(value);
    }
    
    doSomething(printToConsole);
    ```

    > Note that the parameter name is **required**. The function type `(string) => void` means “a function with a parameter named `string` of type `any`“!
    >
    > 
    >
    > 【注意】声明函数类型时，形参一定要写！！！不像C语言中函数的声明可以只写类型，不写形参，[TypeScript中的函数声明一定是要写上形参的](#)

    > 函数类型表达式（Function Type Expression），形式类似于箭头函数，用于声明函数类型的变量的类型，如函数的形参本身描述的就是另外一类函数类型就可以用这种

- `Call Signature`（调用签名）

    In JavaScript, functions can have properties in addition to being callable. However, the function type expression syntax doesn’t allow for declaring properties. If we want to describe something callable with properties, we can write a *call signature* in an object type

    Note that the syntax is slightly different compared to a function type expression - use `:` between the parameter list and the return type rather than `=>`.

    ```typescript
    interface Func {
        (value: string): void;		// 注意，这里返回值类型前面用的是冒号`:`
        							// 而不是向右的箭头！！！
        description: string;
    }
    
    function sayHello(name: string): void {
        console.log(`Hello ${name}`);
    }
    
    function anotherSayHello(name: string): void {
        console.log(`Hello ${name}`);
    }
    anotherSayHello.description = '【function anotherSayHello】';
    
    function doSomething(fn: Func): void {
        fn('张三');
    }
    
    doSomething(sayHello);           // 会报错
    doSomething(anotherSayHello);	 // 不会报错
    ```

    > 函数类型表达式仅仅能表示函数的可调用性，但是，有时候，一种函数类型除了可以被调用外，它还能具有一些属性（函数本身也是一种对象），这种时候，单纯的函数类型表达式就不够看了！
    >
    > 
    >
    > 如果我们想要在描述函数签名的同时，描述函数身上所具有的属性，我们可以使用`type`或者`interface`来描述函数的类型（将函数视为对象），这样的方式，不仅能描述函数的签名，同时还能指定其他额外的信息

- `Construct Signatures`（构造函数签名）

    JavaScript functions can also be invoked with the `new` operator. TypeScript refers to these as *constructors* because they usually create a new object. You can write a *construct signature* by adding the `new` keyword in front of a call signature:

    ```typescript
    type SomeConstructor = {
      new (s: string): SomeObject;			// 通过new关键词调用
    };
    ```

    Some objects, like JavaScript’s `Date` object, can be called with or without `new`. You can combine call and construct signatures in the same type arbitrarily:

    ```typescript
    interface CallOrConstruct {
      (n?: number): string;
      new (s: string): Date;				// 可通过new关键字调用
    										// 也可以不使用new关键字调用
    }
    ```

- `Generic Functions`（泛型函数）

    In TypeScript, *generics* are used when we want to describe a correspondence between two values. We do this by declaring a *type parameter* in the function signature:

    ```typescript
    function firstElement<T>(arr: T[]): T | undefined {
      return arr[0];
    }
    ```

    Note that we didn’t have to specify `Type` in this sample. The type was *inferred* - chosen automatically - by TypeScript.

    > TypeScript能够自动推断泛型函数中的参数类型，因此并非总是需要显式指定泛型参数

- `Constraints`（泛型约束）

    We’ve written some generic functions that can work on *any* kind of value. Sometimes we want to relate two values, but can only operate on a certain subset of values. In this case, we can use a *constraint* to limit the kinds of types that a type parameter can accept.

    Let’s write a function that returns the longer of two values. To do this, we need a `length` property that’s a number. We *constrain* the type parameter to that type by writing an `extends` clause:

    ```typescript
    function longest<T extends {length: number;}>(a: T, b: T): T {
    	return a.length>=b.length ? a : b;
    }
    ```

- 使用泛型要特别小心

    ```typescript
    function minimumLength<T extends { length: number }>(
      obj: T,
      minimum: number
    ): T {
      if (obj.length >= minimum) {
        return obj;
      } else {
        return { length: minimum };			// 这里会报错
        // 原因是我们的函数承诺返回类型T，但是，含有number类型的length属性只是
        // 类型T的一个必要的小小条件，类型T可能还需要满足其他条件，并不是说返回的
        // 对象符合这个条件，它的类型就是T了，因此，会报错，因为类型不兼容
      }
    }
    ```

    It might look like this function is OK - `T` is constrained to `{ length: number }`, and the function either returns `Type` or a value matching that constraint. The problem is that the function promises to return the *same* kind of object as was passed in, not just *some* object matching the constraint.

- **书写良好的泛型函数的指导法则：**

    > **Rule**: When possible, use the type parameter itself rather than constraining it

    > **Rule**: Always use as few type parameters as possible

    > **Rule**: If a type parameter only appears in one location, strongly reconsider if you actually need it（**Type Parameters Should Appear Twice**）

- `Optional Parameters`（可选参数）

    ```typescript
    function fn(x?: number) {
        // ...
    }
    
    fn();					// OK
    fn(10);					// OK
    ```

    Although the parameter is specified as type `number`, the `x` parameter will actually have the type `number | undefined` because unspecified parameters in JavaScript get the value `undefined`.

    Note that when a parameter is optional, callers can always pass `undefined`, as this simply simulates a “missing” argument

    > 函数传参时，传递`undefined`给形参相当于未传参

- `Optional Parameters in Callbacks`（回调函数中的可选参数）

    In JavaScript, if you call a function with more arguments than there are parameters, the extra arguments are simply ignored. TypeScript behaves the same way. Functions with fewer parameters (of the same types) can always take the place of functions with more parameters.

    > 【注意】上述规则只在作为函数实参的回调函数中才生效，在正常的函数中，实参数量多于或者少于形参数量都会报错的！然而[在作为回调函数时，参数个数较少的函数实参传递给定义完备（参数个数较多）的函数形参时也是成立的！](#)

    > **Rule**: When writing a function type for a callback, *never* write an optional parameter unless you intend to *call* the function without passing that argument

    > 这里想表达的意思是：当我们需要像数组的`map`方法这样，让传入的回调函数可以取一个、两个、三个参数，**我们不应该定义可选参数，而是应该直接定义参数最多的形式，这种函数类型可以兼容只有一个参数、两个参数的函数类型**

    ```typescript
    function myForEach<T>(arr: T[], callback:(item: T, index: number)=>void): void {
        for (let i=0; i<arr.length; i++) {
            callback(arr[i], i);	// 对于回调函数，TypeScript与JavaScript
            						// 一样，多余的参数会被忽略，因此，这样调用
            						// callback()函数（指的是使用尽可能多的
            						// 参数来调用）是有兼容性的，即使实际传入
            						// 的回调函数没有这么多的参数，也不会出现
            						// 问题，因为多余的参数都被忽略掉了！！！
        }
    }
    
    const arr = [1, 3, 5, 7, 9];
    
    // 下面这两种函数调用都是正确的！！！
    
    myForEach(arr, (item) => {
        console.log(item);
    });
    
    myForEach(arr, (item, index) => {
        console.log(item, index+1);
    });
    ```

- `Function Overloads`（函数重载）

    In TypeScript, we can specify a function that can be called in different ways by writing *overload signatures*. To do this, write some number of function signatures (usually two or more), followed by the body of the function:

    ```typescript
    /* 函数重载 */
    function makeDate(timestamp: number): Date
    function makeDate(m: number, d: number, y: number): Date;
    function makeDate(mOrTimestamp: number, d?: number, y?: number): Date {
      if (d !== undefined && y !== undefined) {
        return new Date(y, mOrTimestamp, d);
      } else {
        return new Date(mOrTimestamp);
      }
    }
    const d1 = makeDate(12345678);		// OK
    const d2 = makeDate(5, 5, 5);		// OK
    const d3 = makeDate(1, 3);			// Failed
    									// 这里挺有意思的！
    									// 如果没有上述的函数签名，仅仅有最下面
    									// 的函数实现，那么这种用法是不会报错的
    									// 但是，有了函数签名之后，这种用法就会
    									// 报错了！！！
    ```

    > - 在函数实现前面加上了函数签名后，函数的所有有效用法都将由函数签名决定，说明**函数签名是对函数实现的一种更为具体的用法约束**！
    > - **函数实现需要兼容前面所有的函数签名**
    > - 函数签名可以有多个，函数实现只能有一个
    > - 函数实现必须仅仅跟在函数签名后面，函数签名和函数实现之间不能有其他任意表达式（之间可以有空行、空格）

    > The signature of the *implementation* is not visible from the outside. When writing an overloaded function, you should always have *two* or more signatures above the implementation of the function.

- Declaring `this` in a Function（声明函数的`this`类型）

- `void` represents the return value of functions which don’t return a value. It’s the inferred type any time a function doesn’t have any `return` statements, or doesn’t return any explicit value from those return statements:

- The special type `object` refers to any value that isn’t a primitive (`string`, `number`, `bigint`, `boolean`, `symbol`, `null`, or `undefined`).

- The `unknown` type represents *any* value. This is similar to the `any` type, but is safer because it’s not legal to do anything with an `unknown` value

    > - `unknown`类型可以代表任何值，但是它无法做任何事（需要通过类型窄化来进一步确定类型）
    > - `any`类型也可以代表任何只，但是它能做任何事
    > - 因此，在程序中，使用`unknown`类型比`any`类型更加安全

- The `never` type represents values which are *never* observed. In a return type, this means that the function throws an exception or terminates execution of the program.

- `never` also appears when TypeScript determines there’s nothing left in a union.

- `Rest Parameters and Arguments`（剩余参数）

- A spread argument must either have a tuple type or be passed to a rest parameter.

    在TypeScript中，下面的代码会报错：

    ```typescript
    const args = [8, 5];
    const angle = Math.atan2(...args);
    // 报错原因就是`...`运算符只能用于Tuple类型，或者说函数的参数必须是剩余参数
    ```

    最简单的解决方案是这样：

    ```typescript
    const args1 = [8, 5] as const;
    const angle1 = Math.atan2(...args1);		// 这时，就不会再报错了
    ```

- `Parameter Destructuring`（参数解构）

    The type annotation for the object goes after the destructuring syntax:

    ```typescript
    function sum({ a, b, c }: { a: number; b: number; c: number }) {
      console.log(a + b + c);			// 参数解构
    }
    
    sum({ a: 10, b: 3, c: 9 });
    ```

- Return type `void`

    Contextual typing with a return type of `void` does **not** force functions to **not** return something. Another way to say this is a contextual function type with a `void` return type (`type voidFunc = () => void`), when implemented, can return *any* other value, but it will be ignored.

    Thus, the following implementations of the type `() => void` are valid:

    ```typescript
    type voidFunc = () => void;
     
    const f1: voidFunc = () => {
      return true;
    };
     
    const f2: voidFunc = () => true;
     
    const f3: voidFunc = function () {
      return true;
    };
    ```

    And when the return value of one of these functions is assigned to another variable, it will retain the type of `void`:

    ```typescript
    const v1 = f1();
     
    const v2 = f2();
     
    const v3 = f3();
    ```

    This behavior exists so that the following code is valid even though `Array.prototype.push` returns a number and the `Array.prototype.forEach` method expects a function with a return type of `void`.

    ```typescript
    const src = [1, 2, 3];
    const dst = [0];
     
    src.forEach((el) => dst.push(el));		// 因为有这种特性存在，所以这里
    										// 才不会报错！！！
    ```

    There is one other special case to be aware of, when a literal function definition has a `void` return type, that function must **not** return anything.

    ```typescript
    function f2(): void {
      // @ts-expect-error
      return true;
    }
     
    const f3 = function (): void {
      // @ts-expect-error
      return true;
    };
    ```

    > 正是因为函数的返回值为`void`时会有一些这样的特性，因此，`() => undefined`和`() => void`还是有区别的，前者就没有这些特性（应该吧...）