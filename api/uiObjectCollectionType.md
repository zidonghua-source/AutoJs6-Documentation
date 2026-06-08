# UiObjectCollection

UiObjectCollection represents a collection of [UiObject](uiObjectType) instances.

---

<p style="font: bold 2em sans-serif; color: #FF7043">UiObjectCollection</p>

---

## [@] UiObjectCollection

**`Global`**

AutoJs6 中几乎所有 UiObjectCollection 实例均已借助 Rhino 引擎将其包装为了 NativeArray 类型.  
因此 JavaScript 的 Array 原型方法在 UiObjectCollection 实例上可以直接使用:

```js
let wc = contentMatch(/.+/).find();
wc.toArray().forEach(w => console.log(w.content()));
wc.forEach(w => console.log(w.content())); /* 效果同上. */

/* 包装后的对象 "是" 一个 JavaScript 数组. */
console.log(Array.isArray(wc)); // true

/* Array 的原型方法 slice. */
console.log(typeof wc.slice); // 'function'
console.log(wc.slice === Array.prototype.slice); // true

/* UiObjectCollection "类" 的实例方法依然全部可用 (如 size, click, each 等). */
console.log(typeof wc.size); // 'function'
console.log(typeof wc.click); // 'function'
console.log(typeof wc.each); // 'function'
```

经过包装的 UiObjectCollection 将不能通过 instanceof 判断其类型, 但仍可通过 getClass 方法判断:

```js
let wc = contentMatch(/.+/).find();
console.log(wc instanceof UiObjectCollection); // false
console.log(wc.getClass() === UiObjectCollection); // true
```

除上述 find 方法, children, untilFind, findOf 以及附带集合类结果筛选器的 pickup, 返回的也都是一个经过包装的 UiObjectCollection:

```js
let s = contentMatch(/.+/);
let w = pickup(s);
let wcList = [
    s.find(),
    s.untilFind(),
    s.findOf(w && w.compass('p2') || pickup()),
    pickup(s, '{}'),
];
console.log(wcList.every(o => o.getClass() === UiObjectCollection)); // true
```

当 pickup 使用 children 等作为结果筛选器时, 返回的是不经过包装的 UiObjectCollection, 因此需要使用一次 toArray 方法才能使用 JavaScript 的数组相关方法:

```js
let wc = pickup(/.+/, 'p', 'children');
/* 需使用 toArray 进行一次转换. */
wc.toArray().forEach(w => console.log(w.content()));

/* 直接使用 children 方法则不需要 toArray 转换. */
pickup(/.+/, 'p').children().forEach( /* ... */ );
```

UiObjectCollection 可能为空集合:

```js
/* 空集合. */
let wc = contentMatch(/[^\s\S]/).find();

console.log(wc.length); // 0

/* 即使是空集合, 依然是 UiObjectCollection 类型. */
console.log(wc === null); // false
console.log(wc.getClass() === UiObjectCollection); // true
```

集合的遍历即可用 UiObjectCollection 的实例方法 (如 each), 或使用 JavaScript 的数组遍历方法 (如 forEach), 或使用 [ for / for...in (不推荐) / for...of ] 循环:

```js
/**
 * @type {UiObjectCollection | Array<UiObject>}
 */
let wc = pickup(/.+/, 'wc');

wc.each(w => console.log(detect(w, 'txt')));

wc.forEach(w => console.log(detect(w, 'txt')));

for (let i = 0; i < wc.length; i += 1) {
    console.log(detect(wc[i], 'txt'));
}

for (let i in wc) {
    if (wc.hasOwnProperty(i) && /^\d+$/.test(i)) {
        console.log(detect(wc[i], 'txt'));
    }
}

for (let w of wc) {
    console.log(detect(w, 'txt'));
}
```

UiObjectCollection supports [UiObject Actions](uiObjectActionsType).  
Such as [click / longClick / imeEnter / setText / focus], etc.

Source summary of performAction:

```kotlin
/* Updated as of Nov 2, 2022. */

override fun performAction(action: Int, vararg arguments: ActionArgument): Boolean {
    var success = true
    nodes.filterNotNull().forEach { node ->
        when (arguments.isEmpty()) {
            true -> node.performAction(action)
            else -> node.performAction(action, *arguments)
        }.also { success = success and it }
    }
    return success
}
```

From the source summary, when a UiObjectCollection performs an action, it is equivalent to each control in the collection performing the action in turn:

```js
let wc = contentMatch(/[^\s\S]/).find();

/* Perform the click action on the UiObjectCollection. */
wc.click();

/* Equivalent to performing the action on each control element in the collection. */
wc.forEach(w => {
    if (w !== null) {
        w.click();
    }
});
```

After performing the action, the return result is of type [boolean](dataTypes#boolean), indicating that no failure or exception occurred for any control in the collection during the action execution.

Common related methods or properties:

- [UiObject#find](uiObjectType#m-find)
- [UiObject#children](uiObjectType#m-children)
- [UiSelector#find](uiSelectorType#m-find)
- [UiSelector#untilFind](uiSelectorType#m-untilfind)
- [UiSelector.pickup](uiSelectorType#m-pickup)

## [m#] isEmpty

### isEmpty()

**`6.2.0`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

返回集合是否为空.

## [m#] isNotEmpty

### isNotEmpty()

**`6.2.0`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

返回集合是否非空.

## [m#] empty

### empty()

**`DEPRECATED`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

返回集合是否为空.

已弃用, 建议使用 [isEmpty](#m-isempty) 替代.

## [m#] nonEmpty

### nonEmpty()

**`DEPRECATED`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

返回集合是否非空.

已弃用, 建议使用 [isNotEmpty](#m-isnotempty) 替代.

## [m#] toArray

### toArray()

- <ins>**returns**</ins> { [JavaArray](dataTypes#javaarray)<[UiObject](uiObjectType)> }

Convert the collection to a [Java Array](dataTypes#javaarray).

## [m#] toList

### toList()

**`6.2.0`**

- <ins>**returns**</ins> { [JavaArrayList](dataTypes#javaarraylist)<[UiObject](uiObjectType)> }

Convert the collection to a [Java ArrayList](dataTypes#javaarraylist).

## [m#] get

### get(i)

**`DEPRECATED`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) }

Get the UiObject element at the specified index in the collection.

Deprecated, it is recommended to access elements using array subscript notation.

```js
let wc = pickup(/.+/, '{}');
if (wc.length >= 2) {
    console.log(wc.get(2) instanceof UiObject); // true
    console.log(wc[2] instanceof UiObject); // true
}
```

## [m#] size

### size()

**`DEPRECATED`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) }

Return the size of the collection.

Deprecated, it is recommended to use the length property.

```js
let wc = pickup(/.+/, '{}');
console.log(wc.size()); // e.g. 23
console.log(wc.length); // e.g. 23
```

## [m#] each

### each(consumer)

**`DEPRECATED`**

- **consumer** { [(](dataTypes#function)w: [UiObject](uiObjectType)[)](dataTypes#function) [=>](dataTypes#function) [void](dataTypes#void) } - Consumer
- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

Execute consumption once for each element in the collection.

Deprecated, it is recommended to use [forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach).

```js
let wc = pickup(/.+/, '{}');
wc.each(w => console.log(w.content()));
wc.forEach(w => console.log(w.content()));
```

## [m#] find

### find(selector)

**`A11Y`**

- **selector** { [UiSelector](uiSelectorType) } - Selector
- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

Filter a new UiObjectCollection.

Using each element in the current collection as the root node, sequentially filter all descendant nodes that satisfy the selector conditions and add them to a new collection, which is returned as the result.

```js
/* For example, this collection has 3 controls in total. */
let wc = pickup(/.+/);
console.log(wc.length); // 3

/* The 3 controls as root nodes have 10, 50, and 200 descendant nodes respectively. */
console.log(wc.map(w => w.find().length)); // [ 10, 50, 200 ]

/* Among them, the number of controls with clickable true are 2, 3, and 4 respectively. */
console.log(wc.map(w => w.find().filter(c => c.clickable()).length)); // [ 2, 3, 4 ]

/* Therefore wc.find(clickable(true)) should return 2 + 3 + 4. */
console.log(wc.find(clickable(true)).length); // 9
```

## [m#] findOne

### findOne(selector)

**`A11Y`**

- **selector** { [UiSelector](uiSelectorType) } - Selector
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Filter a single control.

Using each element in the collection as the root node, traverse all its descendant nodes. When a node satisfying the selector's filter condition is found, return that control and stop filtering.  
Return null if no control satisfies the filter condition.

```js
let wc = pickup(/.+/);
console.log(wc.findOne(clickable(true))); /* Return a clickable control or null. */
```

## [m#] performAction

Used to perform actions on the UiObjectCollection.

All controls in the collection will perform the specified action.

### performAction(action, ...arguments)

**`A11Y`**

- **action** { [number](dataTypes#number) } - The unique identifier of the action (Action ID)
- **arguments** { [...](documentation#varargs)[ActionArgument](uiObjectActionsType#i-actionargument)[[]](documentation#varargs) } - Action arguments, used to pass parameters to the action
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Return whether all actions were executed successfully.

> Note: Even if one control fails to execute during the process, subsequent controls will continue to perform the action instead of terminating immediately.

> See also: [UiObjectActions](uiObjectActionsType) chapter.

## [m#] click

### click()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Click] action](uiObjectActionsType#m-click).

## [m#] longClick

### longClick()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Long Click] action](uiObjectActionsType#m-longclick).

## [m#] accessibilityFocus

### accessibilityFocus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Get Accessibility Focus] action](uiObjectActionsType#m-accessibilityfocus).

## [m#] clearAccessibilityFocus

### clearAccessibilityFocus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Clear Accessibility Focus] action](uiObjectActionsType#m-clearaccessibilityfocus).

## [m#] focus

### focus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Get Focus] action](uiObjectActionsType#m-focus).

## [m#] clearFocus

### clearFocus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Clear Focus] action](uiObjectActionsType#m-clearfocus).

## [m#] dragStart

### dragStart()

**`6.2.0`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Drag Start] action](uiObjectActionsType#m-dragstart).

## [m#] dragDrop

### dragDrop()

**`6.2.0`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Drag Drop] action](uiObjectActionsType#m-dragdrop).

## [m#] dragCancel

### dragCancel()

**`6.2.0`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Drag Cancel] action](uiObjectActionsType#m-dragcancel).

## [m#] imeEnter

### imeEnter()

**`6.2.0`** **`A11Y`** **`API>=30`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[IME Enter Key] action](uiObjectActionsType#m-imeenter).

## [m#] moveWindow

### moveWindow(x, y)

**`6.2.0`** **`A11Y`** **`API>=26`**

- **x** { [number](dataTypes#number) } - X coordinate
- **y** { [number](dataTypes#number) } - Y coordinate
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Move Window to New Position] action](uiObjectActionsType#m-movewindow).

## [m#] nextAtMovementGranularity

### nextAtMovementGranularity(granularity, isExtendSelection)

**`6.2.0`** **`A11Y`**

- **granularity** { [number](dataTypes#number) } - Granularity
- **isExtendSelection** { [boolean](dataTypes#boolean) } - Whether to extend text selection
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Move to Next Position by Granularity] action](uiObjectActionsType#m-nextatmovementgranularity).

## [m#] nextHtmlElement

### nextHtmlElement(element)

**`6.2.0`** **`A11Y`**

- **element** { [string](dataTypes#string) } - Element name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Move to Next Position by Element] action](uiObjectActionsType#m-nexthtmlelement).

## [m#] pageLeft

### pageLeft()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Page Left to Move View] action](uiObjectActionsType#m-pageleft).

## [m#] pageUp

### pageUp()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Page Up to Move View] action](uiObjectActionsType#m-pageup).

## [m#] pageRight

### pageRight()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Page Right to Move View] action](uiObjectActionsType#m-pageright).

## [m#] pageDown

### pageDown()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Page Down to Move View] action](uiObjectActionsType#m-pagedown).

## [m#] pressAndHold

### pressAndHold()

**`6.2.0`** **`A11Y`** **`API>=30`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Press and Hold] action](uiObjectActionsType#m-pressandhold).

## [m#] previousAtMovementGranularity

### previousAtMovementGranularity(granularity, isExtendSelection)

**`6.2.0`** **`A11Y`**

- **granularity** { [number](dataTypes#number) } - Granularity
- **isExtendSelection** { [boolean](dataTypes#boolean) } - Whether to extend text selection
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Move to Previous Position by Granularity] action](uiObjectActionsType#m-previousatmovementgranularity).

## [m#] previousHtmlElement

### previousHtmlElement(element)

**`6.2.0`** **`A11Y`**

- **element** { [string](dataTypes#string) } - Element name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Move to Previous Position by Element] action](uiObjectActionsType#m-previoushtmlelement).

## [m#] showTextSuggestions

### showTextSuggestions()

**`6.2.0`** **`A11Y`** **`API>=33`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Show Text Suggestions] action](uiObjectActionsType#m-showtextsuggestions).

## [m#] showTooltip

### showTooltip()

**`6.2.0`** **`A11Y`** **`API>=28`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Show Tooltip] action](uiObjectActionsType#m-showtooltip).

## [m#] hideTooltip

### hideTooltip()

**`6.2.0`** **`A11Y`** **`API>=28`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Hide Tooltip] action](uiObjectActionsType#m-hidetooltip).

## [m#] show

### show()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Show in View] action](uiObjectActionsType#m-show).

## [m#] dismiss

### dismiss()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action was fully executed without exceptions during execution

The UiObjectCollection performs the [[Dismiss] action](uiObjectActionsType#m-dismiss).

## [m#] copy

### copy()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 复制文本 ] 行为](uiObjectActionsType#m-copy).

## [m#] cut

### cut()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 剪切文本 ] 行为](uiObjectActionsType#m-cut).

## [m#] paste

### paste()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 粘贴文本 ] 行为](uiObjectActionsType#m-paste).

## [m#] select

### select()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 选中 ] 行为](uiObjectActionsType#m-select).

## [m#] expand

### expand()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 展开 ] 行为](uiObjectActionsType#m-expand).

## [m#] collapse

### collapse()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 折叠 ] 行为](uiObjectActionsType#m-collapse).

## [m#] scrollLeft

### scrollLeft()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 使视窗左移的滚动 ] 行为](uiObjectActionsType#m-scrollleft).

## [m#] scrollUp

### scrollUp()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 使视窗上移的滚动 ] 行为](uiObjectActionsType#m-scrollup).

## [m#] scrollRight

### scrollRight()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 使视窗右移的滚动 ] 行为](uiObjectActionsType#m-scrollright).

## [m#] scrollDown

### scrollDown()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 使视窗下移的滚动 ] 行为](uiObjectActionsType#m-scrolldown).

## [m#] scrollForward

### scrollForward()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 使视窗前移的滚动 ] 行为](uiObjectActionsType#m-scrollforward).

## [m#] scrollBackward

### scrollBackward()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 使视窗后移的滚动 ] 行为](uiObjectActionsType#m-scrollbackward).

## [m#] scrollTo

### scrollTo(row, column)

**`A11Y`**

- **row** { [number](dataTypes#number) } - 行序数
- **column** { [number](dataTypes#number) } - 列序数
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 将指定位置滚动至视窗内 ] 行为](uiObjectActionsType#m-scrollto).

## [m#] contextClick

### contextClick()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 上下文点击 ] 行为](uiObjectActionsType#m-contextclick).

## [m#] setText

### setText(text)

**`A11Y`**

- **text** { [string](dataTypes#string) } - 文本
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 设置文本 ] 行为](uiObjectActionsType#m-settext).

## [m#] setSelection

### setSelection(start, end)

**`A11Y`**

- **start** { [number](dataTypes#number) } - 开始位置
- **end** { [number](dataTypes#number) } - 结束位置
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 选择文本 ] 行为](uiObjectActionsType#m-setselection).

## [m#] clearSelection

### clearSelection()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 取消选择文本 ] 行为](uiObjectActionsType#m-clearselection).

## [m#] setProgress

### setProgress(progress)

**`A11Y`**

- **progress** { [number](dataTypes#number) } - 进度值
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - 是否行为已全部执行且执行过程中无异常

控件集合执行 [[ 设置进度值 ] 行为](uiObjectActionsType#m-setprogress).

## [m] of

### of(list)

- **list** { [UiSelector](uiSelectorType)[[]](dataTypes#array) } - 控件数组
- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

将控件数组转换为 [UiObjectCollection](uiObjectCollectionType).

```js
let wA = pickup(/hello.+/);
let wB = pickup({ clickable: true });

let wc = UiObjectCollection.of([ wA, wB ]);

/* 对 UiObjectCollection 进行操作. */
wc.click();
```