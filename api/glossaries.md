# Glossaries

---

<p style="font: italic 1em sans-serif; color: #78909C">This section is to be supplemented or improved...</p>
<p style="font: italic 1em sans-serif; color: #78909C">Marked by SuperMonster003 on Oct 22, 2022.</p>

---

## Built-in Modules

AutoJs6 built-in modules refer to JavaScript modules that can be used globally in scripts.  
Most of these modules are already listed in the documentation, such as `app`, `images`, `device`, etc.

### Viewing Built-in Module Source Code

In addition to [directly viewing the open-source code](http://project.autojs6.com/tree/master/app/src/main/assets/modules), you can also extract the built-in modules to local storage for viewing:  
Download the [AutoJs6 APK](http://download.autojs6.com) and use compression software to extract the `\assets\modules` folder inside the APK to your local machine.  
Modules are usually named in the format `__%name%__.js`, where `%name%` corresponds to the module name.  
You can view the module source code using a text editor or similar software.

### Modifying or Adding Built-in Modules

> Note: This section may require users to have some programming foundation and development experience.

> Note: This operation requires repackaging to generate a `new AutoJs6 APK` (referred to below as the `new APK`).  
> Because the package name of the `new APK` changes, you must uninstall the previously installed `open-source AutoJs6 APK` (referred to below as the `open-source APK`) before installing the `new APK`.  
> When a new version of the `open-source APK` is released, you must also uninstall the `new APK` in order to install the new version of the `open-source APK`.  
> At that point, any modified or added built-in modules will become invalid.  
> If you wish to integrate your own code into the `open-source APK`, you can submit a [Pull Request (PR)](http://pr.autojs6.com) to the open-source project.

Clone the [AutoJs6 source code](http://project.autojs6.com).  
Open it with [Android Studio](https://developer.android.com/studio/archive) and complete the project build.  
Locate the `\app\src\main\assets\modules` directory.

#### Modifying a Module

After modifying the module code in the directory, directly package it to generate a new APK.

#### Adding a Module

As an example, let's add a `date` module that has a `date.toFullTimeString()` method.

Create a new file `__date__.js` in the `\app\src\main\assets\modules` directory. This file will serve as the added built-in module.

Example file content for reference:

```js
module.exports = function () {
    return {
        toFullTimeString() {
            let now = new Date();
            let pad = x => x.toString().padStart(2, '0');
            return [ now.getHours(), now.getMinutes(), now.getSeconds() ].map(pad).join(':');
        },
    };
};
```

Open the "initialization script", which is `\app\src\main\assets\init.js`.  
Add the date module to the "initialization script":

```js
/* ... */

let $ = {
    /* ... */
    bindModules() {
        _.bind([
            /* ... */

            [ 'date', 'RootAutomator', 'floaty', /* other modules... */ ],

            /* ... */
        ]);
    },
    /* ... */
};

/* ... */
```

After adding it, you can package and generate the new APK.

## Compiler

A syntax compiler is a program capable of reading code line by line.  
It understands how code matches the syntax defined by the programming language and what the code is supposed to do.

## JavaScript Engine

A JavaScript engine is a computer program.  
It receives JavaScript source code and compiles it into binary instructions (machine code) that the CPU can understand.

### Engine and Runtime Environment

The runtime environment is also called the runtime environment. The engine needs to run within a runtime environment.

JavaScript engines are usually developed by browser vendors. Major browsers typically have their own engines:

- Chrome - V8
- Firefox - SpiderMonkey
- IE - Chakra

## Runtime

Also known as `Runtime`.

Runtime is a general term referring to the [libraries / frameworks / platforms] required for code to run.

> See also: [runtime](runtime) (global object)

## Context

Context.

> See also: [context](context) (global object)

## String Pattern

A string that needs to match a specified regular expression.

If the string pattern is `/\d/`, then the given string `str` must satisfy the following statement:

```js
/\d/.test(str) === true;
```

Therefore, the following examples all meet the requirement:  
`'1'`, `'1a'`, `'a1'`, `"hello 2011"`.

String patterns support regular expression [flags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#advanced_searching_with_flags), such as `/hello/i`.

## NaN

NaN stands for "Not A Number".

NaN is a numeric value. In JavaScript, you can detect it using `isNaN` or `Number.isNaN`:

```js
let n = 0 / 0;
isNaN(n); // true
Number.isNaN(n); // true

let m = null;
isNaN(m); // false
Number.isNaN(m); // false

let l = undefined;
isNaN(l); // true
Number.isNaN(l); // false
```

> See also: [MDN #Glossary](https://developer.mozilla.org/en-US/docs/Glossary/NaN) / [MDN #Global Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN) / [isNaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN) / [Number.isNaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN)

## Regular Expression

Also referred to as [ regex / Regular Expression / RegEx / REGEX / RegExp / REX (informal) ], etc.

Regular expression literals in JavaScript are written between a pair of `/` symbols,  
such as `/\d/`, `/^[0-9a-f]{6}$/`, `/[bc]+?(?=y{2,})/i`, etc.

> See also: [MDN #Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)

## Truthy

A truthy value is any value for which `Boolean(truthy)` returns `true`.  
In other words, any value that is not [falsy](#falsy) is truthy.

> See also: [MDN #Glossary](https://developer.mozilla.org/en-US/docs/Glossary/Truthy/)

## Falsy

As of (2022/08), JavaScript has 8 falsy values:

1. false ([boolean](dataTypes#boolean))
2. 0 ([number](dataTypes#number))
3. -0 ([number](dataTypes#number))
4. 0n ([bigint](#bigint))
5. [Empty String](#empty-string)
6. [null](dataTypes#null)
7. [undefined](dataTypes#undefined)
8. [NaN](#nan)

Note that `0` and `-0` are different values:

```js
0 === -0; // true
Object.is(0, -0); // false
Object.is(0n, -0n); // true

let n = -0;
n.toString(); // "0"
Object.is(n, -0) ? `-${n}` : `${n}`; // "-0"
```

> See also: [MDN #Glossary](https://developer.mozilla.org/en-US/docs/Glossary/Falsy/) / [Object.is](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is)

## Empty String

Usually represented by `""`, it is a string data of length 0.

The following representations can all stand for an empty string:

```js
[ "", '', ``, String() ];
```

## BigInt

A numeric type that can represent integers in arbitrary precision format.

Values such as `3n`, `16777216n`, `-1n` are valid.  
Values such as `3.1n`, `2ne5`, `2e5n` are invalid.

> See also: [MDN #Glossary](https://developer.mozilla.org/en-US/docs/Glossary/BigInt) / [MDN #Global Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)

## Enumeration

An enumeration is a way to organize and collect related variables. Many programming languages such as [C / C# / Java] have an enumeration data type.

## Built-in Objects

Also known as [native objects / standard built-in objects]. Built-in objects are independent of the host environment and are provided by the ECMAScript implementation.  
They exist before an ECMAScript program starts executing and are already instantiated; developers do not need to instantiate them again.  
Built-in objects are a subset of native objects. Commonly used ones such as [Object / Function / Array / String / Boolean / Number / Date / RegExp / Error / Math / JSON] are all built-in objects.

> See also: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)

## Built-in Object Extensions

There are mainly two types of extensions to [built-in objects](#built-in-objects): property extensions and prototype extensions.

Property extensions:

```js
Object.saySomething = function (content) {
    console.log(content);
};

Math.sum = function (x, y) {
    return +x + +y;
};
```

Called directly in the form `A.b`:

```js
Object.saySomething("hello"); /* print "hello". */
console.log(Math.sum(2, 3)); // 5
```

Prototype extensions:

```js
Array.prototype.sorted = function () {
    return this.slice().sort();
};
Number.prototype.toFixedNum = function (fraction) {
    return +this.toFixed(fraction);
};
```

Called on the corresponding object instances:

```js
let arr = [ 1, 2, 9, 3 ];
console.log(arr.sorted()); // [ 1, 2, 3, 9 ]
console.log(arr); // [ 1, 2, 9, 3 ]

let num = 375.201;
console.log(num.toFixed(2)); // "375.20"
console.log(num.toFixedNum(2)); // 375.2
```

The above extensions are all custom extensions. They implement custom properties or methods, usually for personal projects.  
Extensions for new features in the ECMAScript specification are called [Polyfill](#polyfill).

> Note: Extending built-in objects is often **dangerous**.
>
> Extending JavaScript native objects means adding properties or methods to their prototypes or the built-in objects themselves.  
> Potential dangers include but are not limited to the following situations:
>
> 1. Unintentionally modifying or overriding JavaScript's standard built-in methods
> 2. Custom extension methods are modified by the definer or collaborating developers, requiring large amounts of dependent code to be changed or even causing errors
> 3. Conflicts with local extension methods of the same name when importing libraries
> 4. Conflicts with extension methods of the same name between multiple imported libraries
> 5. Conflicts with existing extension methods after future standard updates
>
> Therefore, it is recommended to use modular programming instead of object extension.  
> If object extension is truly needed, it is recommended to create a new object with a similar but different name from the native object for extension, as shown in the example below.

The above extension methods can all be implemented in a safer (though potentially more complex to use) way:

```js
let Objectx = {};

Objectx.saySomething = function (content) {
    console.log(content);
};

Objectx.saySomething("hello"); /* print "hello". */

let Mathx = {};

Mathx.sum = function (x, y) {
    return +x + +y;
};

console.log(Mathx.sum(2, 3)); // 5

let Arrayx = {};

Arrayx.sorted = function (arr) {
    return arr.slice().sort();
};

let arr = [ 1, 2, 9, 3 ];
console.log(Arrayx.sorted(arr)); // [ 1, 2, 3, 9 ]

let Numberx = {};

Numberx.toFixedNum = function (num, fraction) {
    return +num.toFixed(fraction);
};

let num = 375.201;
console.log(Numberx.toFixedNum(num, 2)); // 375.2
```

AutoJs6 默认提供了一些内置对象扩展, 如 [ [Arrayx](arrayx), [Numberx](numberx), [Mathx](mathx) ] 等.

这些扩展默认是安全的, 统一为 `Ax.b` 的调用方式,  
如 `Arrayx.intersect`, `Mathx.sum`, `Numberx.clamp`.

```js
console.log(Arrayx.intersect([ 1, 2, 3, 4 ], [ 1, 3, 5 ])); // [ 1, 3 ] 
console.log(Numberx.clamp(Math.random(), [ 0.3, 0.5 ])); // e.g. 0.4251169347959409 
```

The other unsafe type of extension is directly extending built-in objects, which allows more convenient calls:

```js
console.log([ 1, 2, 3, 4 ].intersect([ 1, 3, 5 ])); // [ 1, 3 ]
console.log(Math.random().clamp([ 0.3, 0.5 ])); // e.g. 0.4251169347959409
```

To enable direct extension by default, choose one of the following methods:

- Add the code snippet in the script: `plugins.extendAll();`
- AutoJs6 app settings - Extensibility - JavaScript Built-in Object Extension - [ Enable ]

After direct extension, all extended properties and methods will be attached to the built-in objects or their prototypes as needed. For details, refer to the subsection content of each extension object.  
Direct extension is unsafe and should be used with caution.

> See also: [StackOverflow](https://stackoverflow.com/questions/14034180/why-is-extending-native-objects-a-bad-practice) / [lucybain.com](https://lucybain.com/blog/2014/js-extending-built-in-objects/)

## Polyfill

Also known as [code filler / filler / putty], it is a complete block of code used to provide functional support for environments that do not support new native ECMAScript features.  
See the [Polyfill](polyfill) chapter for details.

## Shim

Also known as [code shim / shim / gap filler], it is a small function library that can be used to intercept API calls or modify incoming parameters, and finally handle the corresponding operation itself or delegate the operation to somewhere else.  
Shims can support old APIs in new environments or new APIs in old environments.  
Some programs are not developed for certain platforms and can also use shims to assist in running.

The difference between Shim and Polyfill can be found in the [Polyfill](polyfill) chapter.

## Application Resources

Application resources refer to additional files and static content used by code, such as [bitmaps / layout definitions / UI strings / animation descriptions], etc.

Usually, application resources are separated from code for independent maintenance.  
Resources can be grouped and placed in specially named resource directories, such as [animator / color / drawable / layout / values / menu], etc.  
At runtime, Android will use appropriate resources based on the current configuration, such as providing different UI layouts according to screen size or different strings according to language settings.

After separating application resources, you can use the [Resource ID](#resource-id) generated in the project's R class to access them.

```js
console.log(context.getString(R.string.text_app_name_powerpoint)); // PowerPoint
console.log(R.id.explorer_item_list); /* e.g. 2131296535 */
console.log(`0x${java.lang.Integer.toHexString(R.id.explorer_item_list)}`); /* e.g. 0x7f090117 */
```

> See also: [Android Docs](https://developer.android.com/guide/topics/resources/providing-resources)

## Resource ID

You can use static integers from subclasses of the R class in code to access [Application Resources](#application-resources):

```js
/* Resource ID is an integer. */
console.log(R.string.text_app_name_autojspro); /* e.g. 2131887020 */
```

Get the type value (string) by resource type:

```js
console.log(context.getString(R.string.text_app_name_autojspro)); /* e.g. AutoJsPro */
```

Get the type value (drawable) by resource type:

```js
/* Draw a light green bell icon. */

'ui';

ui.layout(<vertical bg="#FFFFFF">
    <img id="img" tint="#9CCC65"/>
</vertical>);

ui.img.setImageResource(R.drawable.ic_ali_notification);
```

You can also access `Resource ID` in XML:

```js
/* Draw a light green bell icon. */

'ui';

ui.layout(<vertical bg="#FFFFFF">
    <img id="img" tint="#9CCC65" src="@drawable/ic_ali_notification"/>
</vertical>);
```

Combine the hexadecimal value of the `Resource ID` with the `0x` prefix to use it as the [idHex](uiObjectType#m-idhex) information of a control:

```js
/* Directly combine the Resource ID value. */
console.log(`0x${java.lang.Integer.toHexString(R.id.explorer_item_list)}`); /* e.g. 0x7f090117 */

/* Find the corresponding control on the AutoJs6 home page and get its idHex value. */
console.log(idMatch(/explorer_item_list/).findOnce().idHex()); /* e.g. 0x7f090117 */
```

## Control Hierarchy

Similar to HTML hierarchical rendering, Android's View nesting also forms a hierarchy. The outer view becomes the parent control (Parent Node) of the inner view, and the inner view becomes the child control (Child Node) of the outer view.

In AutoJs6, controls are represented by [UiObject](uiObjectType).

The following methods can obtain the control hierarchy of the current window:

- Use AutoJs6 to obtain it
    - AutoJs6 home page side drawer -> Floating window [Enable] -> Floating icon [Click]
        - Method A: Blue button [Click] -> (Layout range analysis) -> Control diagram [Click] -> View in layout hierarchy
        - Method B: Blue button [Long press] -> Layout hierarchy analysis [Click]

- Use the uiautomatorviewer tool to obtain it
    - Location (Windows example): `"%ANDROID_HOME%\tools\bin\uiautomatorviewer.bat"`

- Use Android Studio's Layout Inspector tool to obtain it
    - Android Studio -> Tools -> Layout Inspector

- Use ADB Shell's dumpsys command to obtain it
    - Use AutoJs6 to execute the code `console.log(shell('dumpsys activity top').result);`

## Collection Info Control

A collection info control refers to a control that has a non-null instance of [AccessibilityNodeInfo.CollectionInfo](https://developer.android.com/reference/android/view/accessibility/AccessibilityNodeInfo.CollectionInfo).

```js
let info = w.getCollectionInfo();
console.log(info);
```

A collection info control contains a series of child controls, distributed in rows and columns similar to an HTML table.  
For example, a vertical list is a collection info control with one column and multiple rows as child controls; a table is also a collection info control with multiple columns and rows as child controls.  
These child controls all have a non-null instance of [AccessibilityNodeInfo.CollectionItemInfo](https://developer.android.com/reference/android/view/accessibility/AccessibilityNodeInfo.CollectionItemInfo):

```js
/* Usually, at least one collection info control can be obtained on the AutoJs6 home page. */
scrollable().find().some((w) => {
    let info = w.getCollectionInfo();
    if (info !== null) {

        /* Display commonly used collection info instance properties or methods. */

        console.log(`rowCount: ${info.getRowCount()}`); /* Corresponds to the w.rowCount() wrapper method. */
        console.log(`columnCount: ${info.getColumnCount()}`); /* Corresponds to the w.columnCount() wrapper method. */

        w.children().forEach((c) => {
            let itemInfo = c.getCollectionItemInfo();
            if (itemInfo !== null) {

                /* Display commonly used collection item info instance properties or methods. */

                console.log(c.bounds());
                console.log(`rowIndex: ${itemInfo.getRowIndex()}`); /* Corresponds to the w.row() wrapper method. */
                console.log(`columnIndex: ${itemInfo.getColumnIndex()}`); /* Corresponds to the w.column() wrapper method. */
                console.log(`rowSpan: ${itemInfo.getRowSpan()}`); /* Corresponds to the w.rowSpan() wrapper method. */
                console.log(`columnSpan: ${itemInfo.getColumnSpan()}`); /* Corresponds to the w.columnSpan() wrapper method. */
                console.log(`selected: ${itemInfo.isSelected()}`);
                console.log(`rowTitle: ${itemInfo.getRowTitle()}`);
                console.log(`columnTitle: ${itemInfo.getColumnTitle()}`);
                console.log('-'.repeat(33));
            }
        });

        return /* @some */ true;
    }
});
```

部分属性或方法:

- `[m#]` getRowCount / `[p#]` rowCount
- `[m#]` getColumnCount / `[p#]` columnCount

常见与信息集存在关联的类:

- android.widget.GridView
- android.widget.ListView
- android.widget.RadioGroup
- com.android.systemui.qs.TileLayout
- androidx.recyclerview.widget.RecyclerView

## 子项信息集控件

子项信息集控件指拥有 [无障碍节点子项信息集 (AccessibilityNodeInfo.CollectionItemInfo)](https://developer.android.com/reference/android/view/accessibility/AccessibilityNodeInfo.CollectionItemInfo) 实例的一组控件, 它们共同属于同一个 [信息集控件](#信息集控件).

部分属性或方法:

- `[m#]` getRowIndex / `[p#]` rowIndex
- `[m#]` getColumnIndex / `[p#]` columnIndex
- `[m#]` getRowSpan / `[p#]` rowSpan
- `[m#]` getColumnSpan / `[p#]` columnSpan
- `[m#]` isSelected / `[p#]` selected
- `[m#]` getRowTitle / `[p#]` rowTitle
- `[m#]` getColumnTitle / `[p#]` columnTitle

## 控件矩形外展

[控件矩形](androidRectType) 边界为非整数时, 外展将对各个边界做如下取整操作:

- left - 左边界左移, 即向下取整, 类似 JavaScript 语言的 Math.floor(left)
- top - 上边界上移, 即向下取整, 类似 JavaScript 语言的 Math.floor(top)
- right - 右边界右移, 即向上取整, 类似 JavaScript 语言的 Math.ceil(right)
- bottom - 下边界下移, 即向上取整, 类似 JavaScript 语言的 Math.ceil(bottom)

例如:

`Rect(10.9, 12.6 - 120.37, 1882.02)` 外展后得到  
`Rect(10, 12, 121, 1883)`

> 注: "外展" 源自健身术语.

## 控件矩形内收

[控件矩形](androidRectType) 边界为非整数时, 外展将对各个边界做如下取整操作:

- left - 左边界右移, 即向上取整, 类似 JavaScript 语言的 Math.ceil(left)
- top - 上边界下移, 即向上取整, 类似 JavaScript 语言的 Math.ceil(top)
- right - 右边界左移, 即向下取整, 类似 JavaScript 语言的 Math.floor(right)
- bottom - 下边界上移, 即向下取整, 类似 JavaScript 语言的 Math.floor(bottom)

例如:

`Rect(10.9, 12.6 - 120.37, 1882.02)` 内收后得到  
`Rect(11, 13, 120, 1882)`

> 注: "内收" 源自健身术语.

## 阈值

阈值, 英文 threshold, 也称 "临界值".  
阈值是令对象发生某种变化所需某种条件的值.

在 AutoJs6 中, 图像与颜色相关的许多方法, 均支持通过参数传入不同类型和数值的阈值.

阈值的范围通常为 `IntRange[0..255]` 和 `Range[0..1]`.

### 相似度

阈值通常可与 `相似度 (Similarity)` 进行转换, 作为参数时通常也支持互相替代:

```text
%Similarity% = 1 - %Threshold% / 255
%Threshold% = (1 - %Similarity%) * 255
```

`阈值 0` 等效于 `相似度 1` (完全匹配, 不允许丝毫误差)  
`阈值 4` 约等效于 `相似度 0.984` (匹配时可以容忍一点误差)  
`阈值 128` 等效于 `相似度 0.5` (匹配时误差容忍相对宽松)  
`阈值 255` 等效于 `相似度 0` (完全容忍, 不常用)

### 颜色匹配阈值

取值范围: IntRange[0..255]

参数类型与此类阈值相关的常用方法:

- [colors.isSimilar](color#m-issimilar)
- images.findColor
- images.findColorInRegion
- images.findMultiColors
- images.detectsColor

### 图像匹配阈值

取值范围: Range[0..1]

参数类型与此类阈值相关的常用方法:

- images.findImage
- images.findImageInRegion
- images.matchTemplate

### 图像阈值化阈值

取值范围: IntRange[0..255]

参数类型与此类阈值相关的常用方法:

- images.threshold(a, b, <i><strong>threshold</strong></i>, c)
- images.adaptiveThreshold ... (此处内容待完善)

## 亮度

亮度既可指物理上对于光的量度, 也可指颜色上色彩的明亮程度.

Luminance, Lightness 和 Brightness 都与 "亮度" 有关.

|            术语             | 常用译名 | 性质  | 可测量或计算 |
|:-------------------------:|:----:|:---:|:------:|
|  [Luminance](#luminance)  |  亮度  | 物理量 |   √    |
| [Brightness](#brightness) | 视亮度  | 感知量 |   ×    |
|  [Lightness](#lightness)  |  明度  | 感知量 |   ×    |

### Luminance

在光度学和色度学中, 亮度 (luminance) 表示人眼对光强度实际感受的物理量, 即单位面积看上去有多明亮.

国际单位制规定亮度的符号是 `Lv`, 单位为 `坎德拉每平方米 (cd/m²)`, 另一个常用非国际单位为 `尼特 (nit)`.  
亮度是一个物理量, 它可被测量及计算.

[Lightness](#lightness) 和 [Brightness](#brightness) 用于表示人眼对光亮的实际感受.  
这个感受是一个感知量, 与物理量不同, 感知量不可测量, 也不可计算.

相同的食盐, 不同人品尝有不同的咸度感受; 同样地, 相同的颜色, 不同人观察也会有不同的亮度感受.

与 Luminance 相关的参考资料:

- 亮度 (Luminance) - [Wikipedia (英)](https://en.wikipedia.org/wiki/Luminance)

### Brightness

视亮度 (Brightness) 是对于光源或物体表面明暗的视知觉特性, 是一个感知量.  
视亮度是视觉的特性, 对视觉目标的辐射或反射的光亮度的感知.  
这种感知对于光的亮度不是线性的, 而是依赖于视觉环境.

与 Brightness 相关的参考资料:

- 视亮度 (Brightness) - [Wikipedia (英)](https://en.wikipedia.org/wiki/Brightness)
- 芒克-怀特错觉 (White's Illusion) - [Wikipedia (英)](https://en.wikipedia.org/wiki/White%27s_illusion)
- 侧抑制 (Lateral Inhibition) - [Wikipedia (英)](https://en.wikipedia.org/wiki/Lateral_inhibition)

### Lightness

明度 (Lightness) 是一个物体与同样亮的白色物体相比后的明亮程度.

与 Lightness 相关的参考资料:

- 明度 (Lightness) - [Wikipedia (英)](https://en.wikipedia.org/wiki/Lightness)

## 注入

代码注入 (Code Injection) 是因处理无效数据的而引发的非预期运行结果.

代码注入可被攻击者用来导入代码到某特定的计算机程序, 以改变程序的执行进程或目的.

常用的代码注入包含 [ 脚本注入 (XSS) / SQL 注入 / PHP 注入 / ASP 注入 ] 等.

> 参阅: [Wikipedia (英)](https://en.wikipedia.org/wiki/Code_injection) / [Wikipedia (中)](https://zh.wikipedia.org/wiki/%E4%BB%A3%E7%A2%BC%E6%B3%A8%E5%85%A5)

## 占位符替换参数

AutoJs6 提供了简化的占位符格式化参数功能, 类似 Java 语言的 `String.format` 方法.

```js
console.log('%s 获得了 %d 个奖章', '大卫', 23);
```

上述示例中 `console.log` 方法提供了占位符格式化参数支持, 运行后控制台将显示一条消息, "大卫 获得了 23 个奖章".

其中, `%s` 和 `%d` 是占位符, 分别表示接受字符串类型和数字类型的参数, 因此后面的剩余参数将依次进行占位符替换, 替换时, JavaScript 将进行参数的隐式转换.

AutoJs6 支持的所有占位符如下:

| <span style="white-space:nowrap">占位符</span> | 简述                                                            | 示例                                                                          | 示例结果                                                                     |
|:-------------------------------------------:|---------------------------------------------------------------|-----------------------------------------------------------------------------|--------------------------------------------------------------------------|
|                     %s                      | <span style="white-space:nowrap">字符串占位符</span>                | <span style="white-space:nowrap">"状态: %s", "开启"<br/>"状态: %s", 100</span>    | <span style="white-space:nowrap">"状态: 开启"<br/>"状态: 100"</span>           |
|                     %d                      | <span style="white-space:nowrap">数字占位符</span>                 | <span style="white-space:nowrap">"数量: %d", 5<br/>"数量: %d", "hello"</span>   | <span style="white-space:nowrap">"数量: 5"<br/>"数量: NaN"</span>            |
|                     %j                      | <span style="white-space:nowrap">JSON 对象占位符</span>            | <span style="white-space:nowrap">"o: %j", { a: 1, b: 2 }</span>             | <span style="white-space:nowrap">'o: {"a":1,"b":2}'</span>               |
|                     %%                      | <span style="white-space:nowrap">转义 % 符号<br/>%% 将转换为 %</span> | <span style="white-space:nowrap">"1%% is 0.01"<br/>"1%%%% is 0.0001"</span> | <span style="white-space:nowrap">"1% is 0.01"<br/>"1%% is 0.0001"</span> |

JavaScript 的模板字符串也可以很好地完成占位符格式化功能:

```js
let person = 'John';
let score = 91;
let subject = 'Chinese';

/* 使用占位符替换参数. */
console.log('%s got a %s score of %d', person, subject, score);

/* 使用 JavaScript 模板字符串. */
console.log(`${person} got a ${subject} score of ${score}`);

/* 上述两种方法均可在控制台显示预期输出内容. */
// "John got a Chinese score of 91"
```

## HTTP 标头

参阅 [HTTP 标头](httpHeaderGlossary) 术语章节.

## MIME 类型

参阅 [MIME 类型](mimeTypeGlossary) 术语章节.
