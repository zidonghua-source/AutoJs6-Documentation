# About the Documentation

<!-- type=misc -->

The AutoJs6 documentation includes usage instructions and examples for module APIs.  
The project was forked from [hyb1996/AutoJs-Docs](https://github.com/hyb1996/AutoJs-Docs/) (GitHub).  
Project repository: [SuperMonster003/AutoJs6-Documentation](http://docs-project.autojs6.com) (GitHub).

---

## Documentation Reading Examples

### Basics

#### device.height

`device` represents a global object (which is also a module here).  
`.height` means accessing the `height` member variable of the `device` object.  
For example, `console.log(device.height)` prints the current device height to the console.

#### colors.rgb(red, green, blue)

Similar to `device`, `colors` is a global object.  
`rgb` is the method name, and `.rgb()` calls the `rgb` method on `colors`. The parameters inside the parentheses (such as `red`) are the method arguments.  
For example, `console.log(colors.rgb(255, 128, 64))` prints an RGB color value with red=255, green=128, and blue=64 to the console.

> Note: In most cases, the documentation does not make a strict distinction between "[function](https://developer.mozilla.org/en-US/docs/Glossary/Function)" and "[method](https://developer.mozilla.org/en-US/docs/Glossary/Method)".

### Temporary Scope Objects

Each chapter typically focuses on a specific object as its subject.

For example, the earlier `colors.rgb(red, green, blue)` appears in the [Color](color) chapter.  
Here, `colors` is called the "temporary scope object" for that chapter.  
It can be an object, a function, or even a "class", and is displayed in the docs using __`orange bold`__.

When listing related methods and properties that follow, the object name itself is no longer repeated:

<p style="font: bold 1em sans-serif; color: #FF7043">colors</p>

[m] rgb

rgb(red, green, blue)

... ...

In the example above, `rgb` stands for `colors.rgb`.

### Parameter Types

#### colors.rgb(red, green, blue)

- **red** { [number](dataTypes#number) }
- **green** { [number](dataTypes#number) }
- **blue** { [number](dataTypes#number) }

The content inside "{}" after a parameter describes its type.  
The example above indicates that three parameters of type [number](dataTypes#number) must be provided.  
`colors.rgb(255, 128, 64)` is valid, while `colors.rgb("abc", 128, 64)` may produce unexpected results or throw an exception.

> Note: Clicking a type hyperlink (if present) jumps to the type details page.

### Return Value Type

#### colors.rgb(red, green, blue)

- **red** { [number](dataTypes#number) }
- **green** { [number](dataTypes#number) }
- **blue** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [number](dataTypes#number) }

The content inside "{}" after `returns` describes the return type.  
The example shows that calling the `colors.rgb` method returns data of type [number](dataTypes#number).

### Property Types

#### colors.RED

- { [number](dataTypes#number) }

Property types are wrapped in a pair of curly braces.  
The example indicates that the `RED` property of `colors` holds data of type [number](dataTypes#number).

Object literal types are represented with double curly braces:

- **properties** {{ name: [string](dataTypes#string); age: [number](dataTypes#number) }}

Multi-line form:

- **properties** {{
    - name: [string](dataTypes#string);
    - age: [number](dataTypes#number);
    - laugh(decibel?: [number](dataTypes#number));
- }}

An example variable matching the expectation above:

```js
let o = { name: "David", age: 13 };
```

Accessible properties that have a non-`undefined` default value are indicated with a pair of square brackets when read:

- [ `1200` ] { [number](dataTypes#number) }

The example represents an accessible property with a default value of 1200.

A pair of double square brackets denotes a constant:

- [[ 0.5 ]] { [number](dataTypes#number) }

The example represents a constant property with the value 0.5.

### Method Signatures

Similar to the example in the [Return Value Type](#return-value-type) section above,  
an identifier that includes [method name + parameter types + return type] is called a "method signature".

> Note: The definition of "method signature" above is only intended to help readers understand the documentation and does not guarantee the linguistic accuracy of the term.

### Method Description

#### colors.rgb(red, green, blue)

- __red__ - R (red) channel value  [ A ]
- __green__ - G (green) channel value  [ A ]
- __blue__ - B (blue) channel value  [ A ]
- __@return__ - color value  [ B ]

Obtains the combined color value from the R/G/B channels. [ C ]

```js
[ D ]
colors.rgb(255, 128, 64); // -32704
colors.rgb(255, 128, 64) === 0xFFFF8040 - Math.pow(2, 32); // true
colors.rgb(255, 128, 64) === colors.toInt("#FFFF8040"); // true
colors.rgb(255, 128, 64) === colors.toInt("#FF8040"); // true
```

Meaning of the letter annotations in the example:

- [ A ] - Parameter description
- [ B ] - Return value description
- [ C ] - Method description
- [ D ] - Usage example

### Variadic Parameters

#### files.join(parent, ...child)

In the example above, the `child` parameter is a "variadic parameter" (also called "variable-length parameter" or "rest parameter").  
A variadic parameter can accept any number of arguments (including zero):

```js
let p = files.getSdcardPath();
files.join(p); /* 0 variadic arguments */
files.join(p, 'a'); /* 1 variadic argument */
files.join(p, 'a', 'b', 'c', 'd'); /* 4 variadic arguments */
```

The documentation follows the JSDoc standard for annotating variadic parameters. Pay special attention that the trailing array in JSDoc represents the container that holds the expanded arguments:

```js
/**
 * @param {number} x
 * @param {number} y
 * @param {...number[]} others
 */
function sum(x, y, others) {
    /* ... */
}
```

In the example, the `others` parameter is variadic. `...number[]` means the expected type for each element in `others` is `number` (not `number[]`). The final `[]` represents the "..." container. "..." and "[]" always appear as a pair.

```js
/**
 * @param {number} x
 * @param {number} y
 * @param {...number[][]} others
 */
function sum(x, y, others) {
    /* ... */
}
```

Here `others` expects elements of type `number[]` (not `number[][]`). The final `[]` still represents the "..." container.

```js
/**
 * @param {number} x
 * @param {number} y
 * @param {...number} others
 */
function sum(x, y, others) {
    /* ... */
}
```

The annotation `...number` for the variadic parameter type is also valid; it is actually a shorthand for `...number[]`.  
To avoid ambiguity, the documentation always uses the full form.

As a reminder: for a variadic parameter written as `...(SomeType)[],` treat `...` and `[]` as a single unit. Only the middle part is the expected element type.

### Optional Parameters

#### device.vibrate(text, delay?)

In the example above, the `delay` parameter is optional (marked with `?`).  
Therefore, both of the following calls are valid:

```js
device.vibrate("hello", 2e3); /* 2-second delay. */
device.vibrate("hello"); /* No delay. */
```

Optional parameters are wrapped in `[]` in descriptions:

- **[ delay ]** { [number](dataTypes#number) }

If an optional parameter has a default value, it is marked with `=`:

- **[ delay = 0 ]** { [number](dataTypes#number) }

See [Parameter Default Values](#parameter-default-values) below for details.

### Parameter Default Values

#### device.vibrate(text, delay?)

- **text** { [string](dataTypes#string) } - Text to be converted to Morse code
- **[ delay = 0 ]** { [number](dataTypes#number) } - Vibration delay
- <ins>**returns**</ins> { [void](dataTypes#void) }

The `delay` parameter in the example is both optional (`?`) and has a default value (`=`).  
Therefore the two calls below are equivalent:

```js
device.vibrate("hello");
device.vibrate("hello", 0);
```

> Note: Method signatures containing default value annotations (as shown) are not valid TypeScript syntax. Such signatures are only used within the documentation.
>
> Note: A parameter marked with `=` is always optional. The `?` marker may be omitted in that case, especially when overload signatures are written separately.  
> See "Method Overloads" below for more details.

### Method Overloads

__`Overload 1/17`__

#### pickup(selector, compass, resultType)

__`Overload 2/17`__

#### pickup(selector, compass)

__`Overload 3/17`__

#### pickup(selector, resultType)

... ...

__`Overload 16/17`__

#### pickup(root, selector)

__`Overload 17/17`__

#### pickup()

Methods tagged with `Overload m/n` indicate the ordinal and total count of overloaded variants.  
For example, `Overload 2/3` means this signature describes the 2nd overload out of a total of 3,  
while `Overload 5-6/17` means the current signature covers both the 5th and 6th overloads out of 17 total.

Overloaded methods can be written in a compacted form:

```text
/* Separate form. */
device.vibrate(text)
device.vibrate(text, delay)

/* Combined (compacted) form. */
device.vibrate(text, delay?)

/* Optional parameters usually include the default value. */
device.vibrate(text, delay?)
· [ delay = 0 ] { number }

/* Even without the "?" marker (for the separate form). */
device.vibrate(text, delay)
· [ delay = 0 ] { number }
```

In most cases, the documentation describes overloaded methods in the separate (expanded) form.

### Globalized Methods

__`Global`__

#### images.requestScreenCapture(landscape)

A method tagged with `Global` can be used globally; the module object prefix may be omitted.  
Therefore the two calls below are equivalent:

```js
images.requestScreenCapture(false);
requestScreenCapture(false);
```

### Method Tags

Used as a concise way to express method characteristics:

- `Global`: [Globalized method](#globalized-methods) (the module object prefix can be omitted).
- `Overload 2/3`: [Method overload](#method-overloads) [ the 2nd of 3 total ].
- `Non-UI`: The method cannot be called in UI mode.
- `6.2.0`: The method requires AutoJs6 version [ 6.2.0 or higher ].
- `[6.2.0]`: The starting version in which the method's functionality, result, signature, or usage changed compared to the previous same-named method.
- `API>=29`: The method requires [API level](apiLevel) [ 29 or higher ]. No exception is thrown if the requirement is not met.
- `API>=29!`: The method requires [API level](apiLevel) [ 29 or higher ]. An exception **will** be thrown if the requirement is not met.
- `A11Y`: The method depends on the Accessibility service.
- `A11Y?`: The method may depend on the Accessibility service.
- `Async`: The method executes asynchronously.
- `Async?`: The method may execute asynchronously (controlled by a parameter).
- `Getter`: 仅取值属性, 即使用 Getter 定义的对象属性.
- `Setter`: 仅存值属性, 即使用 Setter 定义的对象属性.
- `Getter/Setter`: 可存值且可取值属性, 即同时使用 Setter 及 Getter 定义的对象属性.
- `Enum`: 枚举类.
- `CONSTANT`: 常量.
- `READONLY`: 只读属性或方法.
- `DEPRECATED`: 已弃用的属性或方法. 表示不推荐使用, 通常会有替代属性或替代方法.
- `ABANDONED`: 已废弃的属性或方法. 表示不再提供功能支持, 使用后功能将无效.
- `xProto`: 针对原型的内置对象扩展.
- `xObject`: 针对对象的内置对象扩展.
- `xAlias`: 内置对象扩展时使用不同的方法或属性名称 (别名).

### 对象标签

用于简便表示对象的属性:

- \[m]: 普通对象方法或类静态成员方法.
    - 例如在 `images` 作为 [临时作用域对象](#临时作用域对象) 时:
    - `[m] captureScreen` 代表 `images.captureScreen` 方法.
- \[m+]: 具有扩展属性的对象方法.
    - 如 auto 本身是一个方法 (或称函数), waitFor 是 auto 的一个扩展方法.
    - 以下两种调用方式均可用: `auto()` 及 `auto.waitFor()`.
- \[p]: 普通对象属性或类静态成员属性或接口变量属性.
    - 例如在 `device` 作为 [临时作用域对象](#临时作用域对象) 时:
    - `[p] height` 代表 `device.height` 属性, 而非方法.
    - 此标签对 [ Getter / Setter / "类" 属性 / 对象属性 / 方法扩展属性 ] 等不作区分.
- \[p+]: 具有扩展属性的对象属性.
    - 如 autojs 是一个对象, version 是 autojs 的扩展属性,
    - 支持 `autojs.version.xxx` 这样的访问方式,
    - 因此 version 属性将被标记为 `[p+]`.
- \[I]: Java 接口.
- \[C]: Java 类或 JavaScript 构造函数.
- \[c]: Java 类的构造方法.
- \[m!]: 抽象方法 (针对接口及抽象类).
- \[m=]: 包含默认实现的抽象方法 (针对接口).
- \[m#]: 类的实例成员方法.
    - 类的静态成员方法用 [m] 标签标记.
    - 例如对于类 `B`, 它有一个实例 `b` (可能通过 `new B()` 等方式获得),
    - `[m#] foo` 和 `[m] bar` 的调用方式分别为
    - `b.foo()` 和 `B.bar()`.
- \[p#]: 类的实例成员属性.
    - 类的静态成员属性依然用 [p] 标签标记.
    - 例如对于类 `F`, 它有一个实例 `f` (可能通过 `new F()` 等方式获得),
    - `[p#] foo` 和 `[p] bar` 的调用方式分别为
    - `f.foo` 和 `F.bar`.
- \[@]: 代表 [临时作用域对象](#临时作用域对象) 自身.
    - 例如在同一个章节中
        - `[@] apple` [1]
        - `apple(c)` [2]
        - `[m] getColor` [3]
        - `getColor()` [4]
        - `[@] banana` [5]
        - `[m] banana` [6]
        - `banana(x)` [7]
        - `banana(x, y)` [8]
    - 这个章节有两个 [临时作用域对象](#临时作用域对象), apple 和 banana, 对应 `[1]` 和 `[5]`.
    - `[2]` 代表 apple 自身可被调用, 且调用方式为 `apple(c)`, 其中 "c" 为参数.
    - `[3]` 代表 apple 的一个方法, 名称为 "getColor",
    - 由 `[4]` 得知, 其调用方式为 `apple.getColor()`.
    - 注意 `[6]` 与 `[2]` 不同:
    - `[6]` 代表 banana 的一个方法, 名称为 "banana",
    - 由 `[7]` 和 `[8]` 得知, 其调用方式有两种,
    - `banana.banana(x)` 和 `banana.banana(x, y)`.

### 成员访问

成员访问用 "." 表示调用关系, 包括 "类" 静态成员访问, 对象成员访问等.  
而实例成员访问则需要 "类" 的实例才能访问, 用 "#" 表示调用关系.  
例如 JavaScript 的 Number 本身是一个 "类", 可用的成员访问方式如下:

```js
Number(2); /* 作为普通函数使用, 无成员访问. */
Number.EPSILON; /* "类" 静态成员访问, 用 "Number.EPSILON" 标识, 标签为 "[p]". */
new Number(2); /* 创建 "类" 实例, 无成员访问. */
new Number(2).toFixed(0); /* 实例成员访问, 用 "Number#toFixed(number)" 标识, 标签为 "[m#]". */
```

实例成员访问示例:

<p style="font: bold 1em sans-serif; color: #FF7043">UiObject</p>

[m#] bounds()

```js
/* 正确访问示例 */

let w = pickup(/.+/); /* w 是 UiObject 的实例. */
if (w !== null) {
    console.log(w.bounds()); /* 访问 UiObject 实例的 bounds 方法. */
}

/* 错误访问示例 */

importClass(org.autojs.autojs.core.automator.UiObject);
console.log(UiObject.bounds()); /* 访问的是类 UiObject 的静态方法 bounds. */
```

### 模板参数

#### foo.bar(a, b)

- **a** { [T](dataTypes#generic) }
- **b** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [T](dataTypes#generic) }
- <ins>**template**</ins> { [T](dataTypes#generic) }

template 标签指示了一个模板参数 `T`, 这个参数可以代表任意一个类型, 如 `string`.

示例 `foo.bar(a, b)` 中, 返回值与参数 `a` 的类型均为 `T`, 因此两者的类型相同.

例如当参数 `a` 传入 `string` 类型时, 返回值也为 `string` 类型:

```js
typeof foo.bar('hello', 3); // string
```

> 参阅: [泛型](dataTypes#generic)

## 声明

当前项目 (文档) 及 [AutoJs6](http://project.autojs6.com) (App) 均为二次开发.  
相对于 [原始 App](https://github.com/hyb1996/Auto.js/), 二次开发的 App 中会增加或修改部分模块功能.  
相对于 [原始文档](https://github.com/hyb1996/AutoJs-Docs/), 二次开发的文档将进行部分增删或重新编写.  
开发者无法保证对 API 的完全理解及文档的无纰漏撰写.  
如有任何不当之处, 欢迎提交 [Issue](http://docs-issues.autojs6.com) 或 [PR](http://docs-pr.autojs6.com).  