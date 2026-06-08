# Control Node (UiObject)

`UiObject` is commonly referred to as [control / node / control node]. It can be thought of as an [AccessibilityNodeInfo](https://developer.android.com/reference/android/view/accessibility/AccessibilityNodeInfo) object wrapped by the Android Accessibility service. It represents a node in the current active window. Through this node, you can retrieve control information or perform control actions, thereby implementing a series of automation operations.

Application interfaces are usually composed of controls. For example, [ImageView](https://developer.android.com/reference/android/widget/ImageView) forms image controls, and [TextView](https://developer.android.com/reference/android/widget/TextView) forms text controls. Different layouts determine the positions of different controls. For instance, [LinearLayout (linear layout)](https://developer.android.com/reference/android/widget/LinearLayout) arranges and displays controls horizontally or vertically, while [AbsListView (list layout)](https://developer.android.com/reference/android/widget/AbsListView) arranges and displays controls in a list format.
Different layout methods form the [control hierarchy](glossaries#control-hierarchy).

Controls have specific properties, which can be divided into two types: state properties and action properties.  
Action properties can be found in the [Control Node Actions (UiObjectActions)](uiObjectActionsType) chapter.  
Access to state properties is encapsulated as method calls. For example, to access a control's class name, you use `w.className()` instead of `w.className`.

> Note: In AutoJs6, [UiObject](uiObjectType) represents a control node. It inherits from [AccessibilityNodeInfoCompat](https://developer.android.com/reference/androidx/core/view/accessibility/AccessibilityNodeInfoCompat), not from [View](https://developer.android.com/reference/android/view/View).

---

<p style="font: bold 2em sans-serif; color: #FF7043">UiObject</p>

---

## [@] UiObject

**`Global`**

To obtain a UiObject, you typically use a [selector](uiSelectorType).

```js
/* Get a UiObject containing any text. */
let w = pickup(/.+/);

/* Returns null if no control matching the filter exists in the active window. */
console.log(w === null);

/* Use the instanceof operator to check if w is an instance of the UiObject "class". */
console.log(w instanceof UiObject);
```

Most instance methods of UiObject (such as parent, child, etc.) return the same type, enabling method chaining:

```js
let w = pickup('hello');
/* Get the 2nd child of the 3rd-level parent of control w. */
w.parent().parent().parent().child(2);
```

## [m#] parent

### parent(i?)

**`[6.3.3]`** **`A11Y`** **`Overload [1-2]/2`**

- **[ i = `1` ]** { [number](dataTypes#number) } - Relative level
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Returns its parent control.

When a level `i` is specified, returns the parent at that corresponding level.

- When `i` is `0`, returns the control itself.
- When `i` is a positive integer, returns the `i`th-level parent.
- When `i` is negative, throws an exception.

```js
let w = pickup(/.+/);
w.parent();
w.parent(1); /* Same as above. */
w.compass('p'); /* Same as above. */
detect(w, 'p'); /* Same as above. */

w.parent().parent().parent();
w.parent(3); /* Same as above. */
w.compass('p3'); /* Same as above. */
detect(w, 'p3'); /* Same as above. */
```

## [m#] child

### child(i)

**`[6.3.3]`** **`A11Y`**

- **i** { [number](dataTypes#number) } - Index
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Returns the child control at index `i`.

- If `i` is a positive integer or 0, returns the child at that positive index.
- If `i` is negative, returns the child at the reverse index.

```js
let w = pickup(/.+/);
w.child(3);
w.compass('c3'); /* Same as above. */
detect(w, 'c3'); /* Same as above. */

w.child(3).child(1);
w.compass('c3c1'); /* Same as above. */
detect(w, 'c3>1'); /* Same as above. */

w.child(-1); /* The last child control. */

w.child(-2); /* The second-to-last child control. */
w.compass('c-2'); /* Same as above. */
detect(w, 'c-2'); /* Same as above. */
```

## [m#] firstChild

### firstChild()

**`6.3.3`** **`A11Y`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) }

Returns the first child control.

Equivalent to `child(0)`.

## [m#] lastChild

### lastChild()

**`6.3.3`** **`A11Y`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) }

Returns the last child control.

Equivalent to `child(-1)`.

## [m#] childCount

### childCount()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the number of child controls of the current node.

Alias properties or methods:

- `[m#]` getChildCount

## [m#] hasChildren

### hasChildren()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the current node has any child nodes.

Equivalent to `childCount() > 0`.

## [m#] children

### children()

**`A11Y`**

- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

Returns the collection of child controls of the current node.

```js
let cc = pickup({ filter: w => w.children().length > 5 }, 'children');

console.log(cc.length); /* e.g. 10 */

cc.forEach((w) => {
    let content = w.content();
    content && console.log(content);
})
```

To get the collection of all descendant controls under the current node, use [UiObject#find()](#m-find).

```js
let w = pickup({ filter: w => w.children().length > 5 });
console.log(w.find().length); /* e.g. 20 */
```

## [m#] sibling

### sibling(i)

**`6.3.3`** **`A11Y`**

- **i** { [number](dataTypes#number) } - Index
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Returns the sibling control at index `i`.

- If `i` is a positive integer or 0, returns the sibling at that positive index.
- If `i` is negative, returns the sibling at the reverse index.

When `i` is the same as [indexInParent()](#m-indexinparent), it returns itself.

```js
let w = pickup(/.+/);
w.sibling(0); /* The 1st sibling (index 0). */
w.compass('s0'); /* Same as above. */
detect(w, 's0'); /* Same as above. */

w.sibling(-2); /* The second-to-last sibling. */
w.compass('s-2'); /* Same as above. */
detect(w, 's-2'); /* Same as above. */
```

To get adjacent siblings, you can use [offset](#m-offset), or [nextSibling](#m-nextsibling) and [previousSibling](#m-previoussibling).

## [m#] firstSibling

### firstSibling()

**`6.3.3`** **`A11Y`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) }

Returns the first sibling control (may be itself).

Equivalent to `sibling(0)`.

## [m#] lastSibling

### lastSibling()

**`6.3.3`** **`A11Y`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) }

Returns the last sibling control (may be itself).

Equivalent to `sibling(-1)`.

## [m#] offset

### offset(i)

**`6.3.3`** **`A11Y`**

- **i** { [number](dataTypes#number) } - Index offset
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Returns the sibling control at the specified index offset `i`.

- When `i` is a positive integer, returns the forward sibling.
- When `i` is a negative integer, returns the backward sibling.
- When `i` is `0`, returns the control itself.

```js
let w = pickup(/.+/);
w.offset(3);
w.compass('s>3'); /* Same as above. */
detect(w, 's>3'); /* Same as above. */

w.offset(-2);
w.compass('s<2'); /* Same as above. */
detect(w, 's<2'); /* Same as above. */
```

To get adjacent sibling controls, in addition to [offset](#m-offset), you can also use [nextSibling](#m-nextsibling) and [previousSibling](#m-previoussibling).

## [m#] nextSibling

### nextSibling()

**`6.3.3`** **`A11Y`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Returns the next sibling control.

Equivalent to `offset(1)`.

## [m#] previousSibling

### previousSibling()

**`6.3.3`** **`A11Y`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Returns the previous sibling control.

Equivalent to `offset(-1)`.

## [m#] siblingCount

### siblingCount()

**`6.3.3`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the total number of sibling controls for the current node (including itself).

`siblingCount` always returns a number greater than or equal to `1`.

## [m#] isSingleton

### isSingleton()

**`6.3.3`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the current node is a singleton node, i.e., it has no siblings other than itself.

Equivalent to `siblingCount() === 1`.

## [m#] siblings

### siblings()

**`6.3.3`** **`A11Y`**

- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

Returns the collection of sibling controls for the current node (including itself).

## [m#] indexInParent

### indexInParent()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the index value of the current node within its parent control.

```js
/* For example, control p has 3 child controls (a, b, c). */

a.indexInParent(); // 0 
p.child(0); /* Corresponds to a. */

console.log(c.indexInParent()); // 2
p.child(2); /* Corresponds to c. */
```

The `indexInParent` method is often used to access nearby or relative sibling nodes:

```js
/* For example, control p has 3 child controls (a, b, c). */

/* c is the adjacent sibling of b (relative index 1). */
p.child(b.indexInParent() + 1); /* Corresponds to c. */
b.compass('s>1'); /* Using compass method, same effect as above. */

/* a is also the adjacent sibling of b (relative index -1). */
p.child(b.indexInParent() - 1); /* Corresponds to a. */
b.compass('s<1'); /* Using compass method, same effect as above. */

/* a is a sibling of c (relative index -2). */
p.child(c.indexInParent() - 2); /* Corresponds to a. */
b.compass('s<2'); /* Using compass method, same effect as above. */
```

Sometimes it is also necessary to get the index of the current node's parent within its own parent:

```js
let p = pickup({ filter: w => w.depth() > 0 && w.parent().indexInParent() > 0 });
console.log(p.parent().indexInParent()); // e.g. 2
```

## [m#] find

### find()

**`Overload 1/2`** **`A11Y`**

- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

Using the current node as the root, returns the collection of all its descendant controls.

Unlike the [children](#m-children) method, `w.children()` returns only direct child controls, while `w.find()` returns the collection of all descendant controls.

```js
let root = depth(0).findOnce();
console.log(root.find().length); // e.g. 500
console.log(root.children().length); // e.g. 2
```

The descendant control collection includes the root node itself:

```js
/* Find a node that has no descendant controls. */
let w = pickup({ filter: w => w.childCount() === 0 });

/* The collection returned by find() includes itself, not an empty collection. */
console.log(w.find().length); // 1
```

Therefore, `Number of N-level descendant control collections` = `Total number of N+1 level descendant controls` + `1`:

```js
let root = depth(0).findOnce();
let sumA = root.find().length;
let sumB = root.children().reduce((sum, c) => sum + c.find().length, 0);
console.log(sumA, sumB); /* sumA and sumB differ by 1. */
```

### find(selector)

**`Overload 2/2`** **`A11Y`**

- **selector** { [selector](uiSelectorType) } - Selector
- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

Treats the current node as the root and returns the collection of all descendant controls that match the given selector.

```js
/* Find all descendant controls under w whose text content is at least 10 characters long. */
console.log(w.find(contentMatch(/\s*.{10,}\s*/)));
```

## [m#] findOne

### findOne(selector)

**`A11Y`**

- **selector** { [selector](uiSelectorType) } - Selector
- <ins>**returns**</ins> { [UiObject](uiObjectType) }

Treats the current node as the root and finds one control among all its descendants that matches the given selector.

```js
/* Find one descendant control under w whose text content is at least 10 characters long. */
console.log(w.findOne(contentMatch(/\s*.{10,}\s*/)));
```

## [m#] bounds

### bounds()

**`A11Y`**

- <ins>**returns**</ins> { [AndroidRect](androidRectType) }

Alias for the method [boundsInScreen](#m-boundsinscreen).

Returns an [AndroidRect](androidRectType) representing the control's position and size relative to the screen.

```js
let bounds = contentMatch(/.+/).findOnce().bounds();
console.log(bounds); // e.g. Rect(0, 48 - 112, 160)
```

Alias properties or methods:

- `[m#]` [boundsInScreen](#m-boundsinscreen)

## [m#] boundsInScreen

### boundsInScreen()

**`A11Y`**

- <ins>**returns**</ins> { [AndroidRect](androidRectType) }

Returns an [AndroidRect](androidRectType) representing the control's relative position and spatial extent on the screen.

```js
let bounds = contentMatch(/.+/).findOnce().boundsInScreen();
console.log(bounds); // e.g. Rect(0, 48 - 112, 160)
```

Alias properties or methods:

- `[m#]` [bounds](#m-bounds)

## [m#] boundsInParent

### boundsInParent()

**`A11Y`**

**`DEPRECATED`**

- <ins>**returns**</ins> { [AndroidRect](androidRectType) }

Returns an [AndroidRect](androidRectType) representing the control's relative position and spatial extent within its parent control.

Because its parent control is actually the result of `View#getParentForAccessibility()` rather than the control's `viewParent`, the result obtained is unreliable.

```js
let bounds = contentMatch(/.+/).findOnce().boundsInParent();
console.log(bounds); // e.g. Rect(0, 0 - 112, 112)
```

## [m#] boundsLeft

### boundsLeft()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the pixel distance from the left edge of the control's rectangle to the left edge of the screen.

```js
let w = pickup(/.+/);
console.log(w.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(w.bounds().left); // e.g. 0
console.log(w.boundsLeft()); // e.g. 0
console.log(w.left()); // e.g. 0
```

## [m#] boundsTop

### boundsTop()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the pixel distance from the top edge of the control's rectangle to the top edge of the screen.

```js
let w = pickup(/.+/);
console.log(w.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(w.bounds().top); // e.g. 48
console.log(w.boundsTop()); // e.g. 48
console.log(w.top()); // e.g. 48
```

## [m#] boundsRight

### boundsRight()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the pixel distance from the right edge of the control's rectangle to the left edge of the screen.

```js
let w = pickup(/.+/);
console.log(w.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(w.bounds().right); // e.g. 112
console.log(w.right()); // e.g. 112
console.log(w.boundsRight()); // e.g. 112
```

## [m#] boundsBottom

### boundsBottom()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the pixel distance from the bottom edge of the control's rectangle to the top edge of the screen.

```js
let w = pickup(/.+/);
console.log(w.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(w.bounds().bottom); // e.g. 160
console.log(w.bottom()); // e.g. 160
console.log(w.boundsBottom()); // e.g. 160
```

## [m#] boundsWidth

### boundsWidth()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the width of the control's rectangle.

```js
let w = pickup(/.+/);
console.log(w.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(w.bounds().width()); // e.g. 112
console.log(w.boundsWidth()); // e.g. 112
console.log(w.right() - w.left()); // e.g. 112
```

## [m#] boundsHeight

### boundsHeight()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the height of the control's rectangle.

```js
let w = pickup(/.+/);
console.log(w.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(w.bounds().height()); // e.g. 112
console.log(w.boundsHeight()); // e.g. 112
console.log(w.bottom() - w.top()); // e.g. 112
```

## [m#] boundsCenterX

### boundsCenterX()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the center X coordinate of the control's rectangle (pixel distance from the center point to the left edge of the screen).

This coordinate is an integer. Non-integer values are processed with **floor rounding**, which results in loss of precision.

If you need to preserve precision, use [boundsExactCenterX](#m-boundsexactcenterx).

```js
let wA = pickup(/.+/);
console.log(wA.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(wA.bounds().centerX()); // e.g. 56
console.log(wA.boundsCenterX()); // e.g. 56

let wB = pickup(/.+/);
console.log(wB.bounds()); // e.g. Rect(0, 0 - 11, 20)
console.log(wB.boundsCenterX()); // e.g. 5 (5.5 floored to 5)

let wC = pickup(/.+/);
console.log(wC.bounds()); // e.g. Rect(0, 0 - -11, 20)
console.log(wC.boundsCenterX()); // e.g. -6 (-5.5 floored to -6)
```

## [m#] boundsExactCenterX

### boundsExactCenterX()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the center X coordinate of the control's rectangle (pixel distance from the center point to the left edge of the screen).

This coordinate preserves precision (may be a non-integer). If you need an integer result, use [boundsCenterX](#m-boundscenterx).

```js
let wA = pickup(/.+/);
console.log(wA.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(wA.bounds().exactCenterX()); // e.g. 56
console.log(wA.boundsExactCenterX()); // e.g. 56

let wB = pickup(/.+/);
console.log(wB.bounds()); // e.g. Rect(0, 0 - 11, 20)
console.log(wB.boundsExactCenterX()); // e.g. 5.5

let wC = pickup(/.+/);
console.log(wC.bounds()); // e.g. Rect(0, 0 - -11, 20)
console.log(wC.boundsExactCenterX()); // e.g. -5.5
```

## [m#] boundsCenterY

### boundsCenterY()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the center Y coordinate of the control's rectangle (pixel distance from the center point to the top edge of the screen).

This coordinate is an integer. Non-integer values are processed with **floor rounding**, which results in loss of precision.

If you need to preserve precision, use [boundsExactCenterY](#m-boundsexactcentery).

```js
let wA = pickup(/.+/);
console.log(wA.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(wA.bounds().centerY()); // e.g. 104
console.log(wA.boundsCenterY()); // e.g. 104

let wB = pickup(/.+/);
console.log(wB.bounds()); // e.g. Rect(0, 0 - 11, 33)
console.log(wB.boundsCenterY()); // e.g. 16 (16.5 floored to 16)

let wC = pickup(/.+/);
console.log(wC.bounds()); // e.g. Rect(0, 0 - 11, -33)
console.log(wC.boundsCenterY()); // e.g. -17 (-16.5 floored to -17)
```

## [m#] boundsExactCenterY

### boundsExactCenterY()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the center Y coordinate of the control's rectangle (pixel distance from the center point to the top edge of the screen).

This coordinate preserves precision (may be a non-integer). If you need an integer result, use [boundsCenterY](#m-boundscentery).

```js
let wA = pickup(/.+/);
console.log(wA.bounds()); // e.g. Rect(0, 48 - 112, 160)
console.log(wA.bounds().exactCenterY()); // e.g. 104
console.log(wA.boundsExactCenterY()); // e.g. 104

let wB = pickup(/.+/);
console.log(wB.bounds()); // e.g. Rect(0, 0 - 11, 33)
console.log(wB.boundsExactCenterY()); // e.g. 16.5

let wC = pickup(/.+/);
console.log(wC.bounds()); // e.g. Rect(0, 0 - 11, -33)
console.log(wC.boundsExactCenterY()); // e.g. -16.5
```

## [m#] left

### left()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the pixel distance from the left edge of the control's rectangle to the left edge of the screen.

Alias of [UiObject#boundsLeft](#m-boundsleft).

## [m#] top

### top()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the pixel distance from the top edge of the control's rectangle to the top edge of the screen.

Alias of [UiObject#boundsTop](#m-boundstop).

## [m#] right

### right()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the pixel distance from the right edge of the control's rectangle to the left edge of the screen.

Alias of [UiObject#boundsRight](#m-boundsright).

## [m#] bottom

### bottom()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the pixel distance from the bottom edge of the control's rectangle to the top edge of the screen.

Alias of [UiObject#boundsBottom](#m-boundsbottom).

## [m#] width

### width()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the width of the control's rectangle.

Alias of [UiObject#boundsWidth](#m-boundswidth).

## [m#] height

### height()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the height of the control's rectangle.

Alias of [UiObject#boundsHeight](#m-boundsheight).

## [m#] centerX

### centerX()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the center X coordinate of the control's rectangle (pixel distance from the center point to the left edge of the screen).

Alias of [UiObject#boundsCenterX](#m-boundscenterx).

## [m#] exactCenterX

### exactCenterX()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the center X coordinate of the control's rectangle (pixel distance from the center point to the left edge of the screen).

Alias of [UiObject#boundsExactCenterX](#m-boundsexactcenterx).

## [m#] centerY

### centerY()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the center Y coordinate of the control's rectangle (pixel distance from the center point to the top edge of the screen).

Alias of [UiObject#boundsCenterY](#m-boundscentery).

## [m#] exactCenterY

### exactCenterY()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the center Y coordinate of the control's rectangle (pixel distance from the center point to the top edge of the screen).

Alias of [UiObject#boundsExactCenterY](#m-boundsexactcentery).

## [m#] point

### point()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [OpenCVPoint](opencvPointType) }

Returns the center point of the control's rectangle ([Point](opencvPointType)).

This center point coordinate is calculated from [exactCenterX](#m-exactcenterx) and [exactCenterY](#m-exactcentery), so precision is preserved.

Alias of [center](#m-center).

```js
let wA = pickup(/.+/);
console.log(wA.bounds()); // e.g. Rect(0, 0 - 10, 12)
console.log(wA.point()); // e.g. {5.0, 6.0}
console.log(wA.point().x); // e.g. 5

let wB = pickup(/.+/);
console.log(wB.bounds()); // e.g. Rect(0, 0 - 11, 13)
console.log(wB.point()); // e.g. {5.5, 6.5}
console.log(wB.point().y); // e.g. 6.5
```

## [m#] center

### center()

**`6.4.2`** **`A11Y`**

- <ins>**returns**</ins> { [OpenCVPoint](opencvPointType) }

Returns the center point of the control's rectangle ([Point](opencvPointType)).

This center point coordinate is calculated from [exactCenterX](#m-exactcenterx) and [exactCenterY](#m-exactcentery), so precision is preserved.

Alias of [point](#m-point).

```js
let wA = pickup(/.+/);
console.log(wA.bounds()); // e.g. Rect(0, 0 - 10, 12)
console.log(wA.center()); // e.g. {5.0, 6.0}
console.log(wA.center().x); // e.g. 5

let wB = pickup(/.+/);
console.log(wB.bounds()); // e.g. Rect(0, 0 - 11, 13)
console.log(wB.center()); // e.g. {5.5, 6.5}
console.log(wB.center().y); // e.g. 6.5
```

## [m#] size

### size()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [OpenCVSize](opencvSizeType) }

Returns the size of the control's rectangle ([Size](opencvSizeType)).

```js
let w = pickup(/.+/);
console.log(w.bounds()); // e.g. Rect(0, 0 - 10, 12)
console.log(w.size()); // e.g. 10x12
console.log(w.size().width); // e.g. 10
console.log(w.size().height); // e.g. 12
```

## [m#] clickBounds

### clickBounds(offsetX?, offsetY?)

**`6.2.0`** **`Overload [1-3]/3`** **`A11Y`**

- **[ offsetX = 0 ]** { [number](dataTypes#number) } - X coordinate offset (supports negative values and percentages)
- **[ offsetY = 0 ]** { [number](dataTypes#number) } - Y coordinate offset (supports negative values and percentages)
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the click action has been executed without exceptions during execution

Clicks at the center point coordinates of the control's rectangle.

The click operation is performed using [automator.click(x, y)](automator#m-click). This operation requires accessibility service to be enabled.

```js
let w = pickup(/.+/);

console.log(w.bounds()); // e.g. Rect(0, 60 - 100, 200)

w.clickBounds(); /* Equivalent to click(50, 130). */
click(w.centerX(), w.centerY()); /* Same effect as above. */

w.clickBounds(10); /* X coordinate offset of 10 pixels, equivalent to click(50 + 10, 130). */
w.clickBounds(10, 15); /* X and Y coordinate offsets of 10 and 15 pixels respectively, equivalent to click(50 + 10, 130 + 15). */
w.clickBounds(0, -15); /* Y coordinate offset of -15 pixels, equivalent to click(50, 130 - 15). */
w.clickBounds(0.2); /* X coordinate offset of 20% of screen width, equivalent to click(50 + 0.2 * device.width, 130). */
w.clickBounds(0.2, -0.05); /* X and Y coordinate offsets of 20% screen width and -5% screen height. */
```

## [m#] id

### id()

**`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) | [null](dataTypes#null) }

Returns the node's Fully-Qualified ID Resource Name.

If the ID does not exist, returns null.

The Android fully-qualified resource name format is `package:type/entry`, i.e., `packageName:type/resourceEntry`.  
For ID resources, the `type` is `id`.  
A valid ID resource name example: `com.test:id/some_entry`.

```js
console.log(idMatch(/.+/).findOnce().id()); // e.g. org.autojs.autojs6:id/action_bar_root
console.log(idMatch(/.+/).findOnce().fullId()); /* Same as above. */
console.log(idMatch(/.+/).findOnce().getViewIdResourceName()); /* Same as above. */
```

Note that some apps' control ID resource names may not follow the standard format:

```js
/* Standard fully-qualified ID. */
let canonicalId = "com.test:id/hello_world";

/* Possible non-standard ID format. */
let peculiarId = "hello_world"; /* Only the resource entry, missing package name and type identifier. */
```

Alias properties or methods:

- `[m#]` getViewIdResourceName
- `[m#]` [fullId](#m-fullid)

## [m#] fullId

### fullId()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) | [null](dataTypes#null) }

Returns the node's Fully-Qualified ID Resource Name.

If the ID does not exist, returns null.

Alias of [UiObject#id](#m-id).

## [m#] idEntry

### idEntry()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) | [null](dataTypes#null) }

Returns the node's ID Resource Entry Name.

The Android fully-qualified resource name format is `package:type/entry`, i.e., `packageName:type/resourceEntry`.  
For example, for the ID resource name `com.test:id/some_entry`, its ID resource entry name is `some_entry`.

```js
/* Fully-qualified ID. */
console.log(idMatch(/.+/).findOnce().id()); // e.g. org.autojs.autojs6:id/action_bar_root

/* ID resource entry name. */
console.log(idMatch(/.+/).findOnce().idEntry()); // action_bar_root
console.log(idMatch(/.+/).findOnce().simpleId()); /* Same as above. */
```

Alias properties or methods:

- `[m#]` [simpleId](#m-simpleid)

## [m#] simpleId

### simpleId()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) | [null](dataTypes#null) }

Returns the node's ID Resource Entry Name.

If the ID does not exist, returns null.

Alias of [UiObject#idEntry](#m-identry).

## [m#] idHex

### idHex()

**`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) | [null](dataTypes#null) }

Returns the hexadecimal string value of the [resource ID](glossaries#resource-id) of the node's [Fully-Qualified ID](#m-fullid), abbreviated as `ID resource hexadecimal representation`.

1. Get the `resource ID` corresponding to the `Fully-Qualified ID`
2. Combine the hexadecimal value of the `resource ID` with the `0x` prefix
3. Return the combined string value

If the ID does not exist, returns null.

```js
console.log(idMatch(/explorer_item_list/).findOnce().idHex()); /* e.g. 0x7f090117 */
```

## [m#] text

### text()

**`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) }

Returns the text content of the control.

If the text content does not exist, returns an empty string.

For privacy protection, password-type controls where `isPassword()` returns `true` will have `text()` return an empty string.

```js
console.log(textMatch(/.+/).findOnce().text()); /* e.g. hello */
```

Alias properties or methods:

- `[m#]` getText

## [m#] desc

### desc()

**`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) | [null](dataTypes#null) }

Returns the content description label of the control.

If the content description label does not exist, returns null.

The content description label helps users who require accessibility services (such as people with visual impairments) understand the purpose or description of the current control.  
For example, when [TalkBack](https://support.google.com/accessibility/android/topic/10601570?hl=en) is enabled, it can read the content description label of controls, which is especially important for understanding controls that have no text content.

```js
console.log(descMatch(/.+/).findOnce().desc()); /* e.g. Restart icon */
```

Alias properties or methods:

- `[m#]` getContentDescription

## [m#] content

### content()

**`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) }

Returns the content of the control (including the content description label or text content).

If there is no content, returns an empty string.

The `content` method is equivalent to `w.desc() || w.text()`, i.e., it prioritizes the content returned by [desc](#m-desc), and if it is null, continues to get the content returned by [text](#m-text).

```js
console.log(contentMatch(/.+/).findOnce().content()); /* e.g. Avatar */
```

## [m#] className

### className()

**`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) | [null](dataTypes#null) }

Returns the class name of the control.

If the class name does not exist, returns null.

```js
console.log(classNameMatch(/.+/).findOnce().className()); /* e.g. android.widget.EditText */
```

Common class names:

- android.view.View
- android.view.ViewGroup
- android.widget.ImageView
- android.widget.ImageButton
- android.widget.Button
- android.widget.ScrollView
- android.widget.TextView
- android.widget.EditText
- android.widget.Switch
- android.widget.LinearLayout
- android.widget.FrameLayout
- android.widget.RelativeLayout

Alias properties or methods:

- `[m#]` getClassName

## [m#] packageName

### packageName()

**`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string) | [null](dataTypes#null) }

Returns the package name of the control.

If the package name does not exist, returns null.

```js
console.log(packageNameMatch(/.+/).findOnce().packageName()); /* e.g. org.autojs.autojs6 */
```

Alias properties or methods:

- `[m#]` getPackageName

## [m#] depth

### depth()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the depth in the [control hierarchy](glossaries#control-hierarchy).

The top-level control (only one) has a depth value of 0, secondary controls (there may be multiple) all have a depth value of 1, and so on.

```js
console.log(findOnce().depth()); // 0
console.log(contentMatch(/.+/).depth()); /* e.g. 5 */
```

## [m#] checkable

### checkable()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is checkable.

Alias properties or methods:

- `[m#]` isCheckable

Associated properties or methods:

- State checking
    - `[m#]` [checked](#m-checked) (isChecked)
- Availability checking
    - `[m#]` [checkable](#m-checkable) (isCheckable)

## [m#] checked

### checked()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is checked.

Alias properties or methods:

- `[m#]` isChecked

Associated properties or methods:

- State checking
    - `[m#]` [checked](#m-checked) (isChecked)
- Availability checking
    - `[m#]` [checkable](#m-checkable) (isCheckable)

## [m#] focusable

### focusable()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is focusable.

Alias properties or methods:

- `[m#]` isFocusable

Associated properties or methods:

- State checking
    - `[m#]` [focused](#m-focused) (isFocused)
- Availability checking
    - `[m#]` [focusable](#m-focusable) (isFocusable)

## [m#] focused

### focused()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is focused.

Alias properties or methods:

- `[m#]` isFocused

Associated properties or methods:

- State checking
    - `[m#]` [focused](#m-focused) (isFocused)
- Availability checking
    - `[m#]` [focusable](#m-focusable) (isFocusable)

## [m#] visibleToUser

### visibleToUser()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is visible to the user.

Alias properties or methods:

- `[m#]` isVisibleToUser

## [m#] accessibilityFocused

### accessibilityFocused()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control has acquired accessibility focus.

Alias properties or methods:

- `[m#]` isAccessibilityFocused

Associated properties or methods:

- State checking
    - `[m#]` [accessibilityFocused](#m-accessibilityfocused) (isAccessibilityFocused)
- Action execution
    - `[m#]` [accessibilityFocus](uiObjectActionsType#m-accessibilityfocus)

## [m#] selected

### selected()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is selected.

Alias properties or methods:

- `[m#]` isSelected

Associated properties or methods:

- State checking
    - `[m#]` [selected](#m-selected) (isSelected)
- Action execution
    - `[m#]` [select](uiObjectActionsType#m-select)

## [m#] clickable

### clickable()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is clickable.

Alias properties or methods:

- `[m#]` isClickable

Associated properties or methods:

- State checking
    - `[m#]` [clickable](#m-clickable) (isClickable)
- Action execution
    - `[m#]` [click](uiObjectActionsType#m-click)

## [m#] longClickable

### longClickable()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is long-clickable.

Alias properties or methods:

- `[m#]` isLongClickable

Associated properties or methods:

- State checking
    - `[m#]` [longClickable](#m-longclickable) (isLongClickable)
- Action execution
    - `[m#]` [longClick](uiObjectActionsType#m-longclick)

## [m#] enabled

### enabled()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is enabled (not disabled).

Alias properties or methods:

- `[m#]` isEnabled

## [m#] password

### password()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is a password-type control.

Alias properties or methods:

- `[m#]` isPassword

## [m#] scrollable

### scrollable()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is scrollable.

Alias properties or methods:

- `[m#]` isScrollable

Associated properties or methods:

- State checking
    - `[m#]` [scrollable](#m-scrollable) (isScrollable)
- Action execution
    - `[m#]` [scrollBackward](uiObjectActionsType#m-scrollbackward)
    - `[m#]` [scrollDown](uiObjectActionsType#m-scrolldown)
    - `[m#]` [scrollForward](uiObjectActionsType#m-scrollforward)
    - `[m#]` [scrollLeft](uiObjectActionsType#m-scrollleft)
    - `[m#]` [scrollRight](uiObjectActionsType#m-scrollright)
    - `[m#]` [scrollTo](uiObjectActionsType#m-scrollto)
    - `[m#]` [scrollUp](uiObjectActionsType#m-scrollup)

## [m#] editable

### editable()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control is editable.

Alias properties or methods:

- `[m#]` isEditable

## [m#] rowCount

### rowCount()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the row count of the [collection info control](glossaries#collection-info-control).

## [m#] columnCount

### columnCount()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the column count of the [collection info control](glossaries#collection-info-control).

## [m#] row

### row()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the row index of the [collection item info control](glossaries#collection-item-info-control).

## [m#] column

### column()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the column index of the [collection item info control](glossaries#collection-item-info-control).

## [m#] rowSpan

### rowSpan()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the number of rows spanned by the [collection item info control](glossaries#collection-item-info-control).

## [m#] columnSpan

### columnSpan()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the number of columns spanned by the [collection item info control](glossaries#collection-item-info-control).

## [m#] drawingOrder

### drawingOrder()

**`A11Y`**

- <ins>**returns**</ins> { [number](dataTypes#number) }

Returns the view drawing order of the node.

This order is determined by its parent node and is an index value relative to its sibling nodes.  
In some cases, the drawing process of Views is essentially simultaneous, so two sibling nodes may return the same index value, or this index value may even be ignored (returning the default value 0).

```js
console.log(pickup(/.+/).drawingOrder()); // e.g. 0
```

## [m#] actionNames

### actionNames()

**`A11Y`**

- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

Returns an array of [control actions](uiObjectActionsType) supported by the control.

```js
let w = pickup(/.+/);

/* e.g. [ ACTION_CLICK, ACTION_SET_SELECTION, ACTION_FOCUS ] */
console.log(w.actionNames());
```

In the example above, the three elements in the array represent the actions the control can perform, i.e., `w.click()`, `w.setSelection(...)`, and `w.focus()`.

The elements in the array are string forms of control action IDs starting with "ACTION_".  
For more control action IDs, see the `Action IDs` table in the [Control Node Actions](uiObjectActionsType) chapter.

To check whether a control supports one or more actions, you can use the [hasAction](#m-hasaction) method.

## [m#] hasAction

### hasAction(...actions)

**`A11Y`**

- **actions** { [...](documentation#variadic-parameter)[string](dataTypes#string)[[]](documentation#variadic-parameter) }
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the control **fully supports** one or more specified [control actions](uiObjectActionsType).

The actions parameter is a [variadic parameter](documentation#variadic-parameter), and each must be a string form of a control action ID starting with "ACTION_" (the "ACTION_" prefix can be omitted).

```js
let w = pickup(/.+/);

/* Check if w is clickable. */
console.log(w.hasAction("ACTION_CLICK"));
console.log(w.hasAction("CLICK")); /* The ACTION_ prefix can be omitted. */

/* Check if w is clickable, focusable, and can set text. */
console.log(w.hasAction("ACTION_CLICK", "ACTION_FOCUS", "ACTION_SET_TEXT"));
console.log(w.hasAction("CLICK", "FOCUS", "SET_TEXT")); /* The ACTION_ prefix can be omitted. */
```

For more control action IDs, see the `Action IDs` table in the [Control Node Actions](uiObjectActionsType) chapter.

## [m#] performAction

Used to execute the specified control action.  
The relevant content has been described in detail in the [Control Node Actions](uiObjectActionsType) chapter; only the signatures of several overload methods are noted here, and the related content will not be repeated.

### performAction(action, ...arguments)

**`Overload 1/2`** **`A11Y`**

- **action** { [number](dataTypes#number) } - Unique identifier of the action (Action ID)
- **arguments** { [...](documentation#variadic-parameter)[ActionArgument](uiObjectActionsType#i-actionargument)[[]](documentation#variadic-parameter) } - Action arguments, used to pass parameters to the action
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

### performAction(action, bundle)

**`Overload 2/2`** **`A11Y`**

- **action** { [number](dataTypes#number) } - Unique identifier of the action (Action ID)
- **bundle** { [AndroidBundle](uiObjectActionsType#i-actionargument) } - Action parameter container, used to pass parameters to the action
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

## [m#] click

### click()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ click ] action](uiObjectActionsType#m-click).

## [m#] longClick

### longClick()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ long click ] action](uiObjectActionsType#m-longclick).

## [m#] accessibilityFocus

### accessibilityFocus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ accessibility focus ] action](uiObjectActionsType#m-accessibilityfocus).

## [m#] clearAccessibilityFocus

### clearAccessibilityFocus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ clear accessibility focus ] action](uiObjectActionsType#m-clearaccessibilityfocus).

## [m#] focus

### focus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ focus ] action](uiObjectActionsType#m-focus).

## [m#] clearFocus

### clearFocus()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ clear focus ] action](uiObjectActionsType#m-clearfocus).

## [m#] dragStart

### dragStart()

**`6.2.0`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ drag start ] action](uiObjectActionsType#m-dragstart).

## [m#] dragDrop

### dragDrop()

**`6.2.0`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ drag drop ] action](uiObjectActionsType#m-dragdrop).

## [m#] dragCancel

### dragCancel()

**`6.2.0`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ drag cancel ] action](uiObjectActionsType#m-dragcancel).

## [m#] imeEnter

### imeEnter()

**`6.2.0`** **`A11Y`** **`API>=30`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ input method ENTER key ] action](uiObjectActionsType#m-imeenter).

## [m#] moveWindow

### moveWindow(x, y)

**`6.2.0`** **`A11Y`** **`API>=26`**

- **x** { [number](dataTypes#number) } - X coordinate
- **y** { [number](dataTypes#number) } - Y coordinate
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ move window to new position ] action](uiObjectActionsType#m-movewindow).

## [m#] nextAtMovementGranularity

### nextAtMovementGranularity(granularity, isExtendSelection)

**`6.2.0`** **`A11Y`**

- **granularity** { [number](dataTypes#number) } - Granularity
- **isExtendSelection** { [boolean](dataTypes#boolean) } - Whether to extend text selection
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ move to next position at granularity ] action](uiObjectActionsType#m-nextatmovementgranularity).

## [m#] nextHtmlElement

### nextHtmlElement(element)

**`6.2.0`** **`A11Y`**

- **element** { [string](dataTypes#string) } - Element name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ move to next element ] action](uiObjectActionsType#m-nexthtmlelement).

## [m#] pageLeft

### pageLeft()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ page left to move viewport ] action](uiObjectActionsType#m-pageleft).

## [m#] pageUp

### pageUp()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ page up to move viewport ] action](uiObjectActionsType#m-pageup).

## [m#] pageRight

### pageRight()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ page right to move viewport ] action](uiObjectActionsType#m-pageright).

## [m#] pageDown

### pageDown()

**`6.2.0`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ page down to move viewport ] action](uiObjectActionsType#m-pagedown).

## [m#] pressAndHold

### pressAndHold()

**`6.2.0`** **`A11Y`** **`API>=30`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ press and hold ] action](uiObjectActionsType#m-pressandhold).

## [m#] previousAtMovementGranularity

### previousAtMovementGranularity(granularity, isExtendSelection)

**`6.2.0`** **`A11Y`**

- **granularity** { [number](dataTypes#number) } - Granularity
- **isExtendSelection** { [boolean](dataTypes#boolean) } - Whether to extend text selection
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ move to previous position at granularity ] action](uiObjectActionsType#m-previousatmovementgranularity).

## [m#] previousHtmlElement

### previousHtmlElement(element)

**`6.2.0`** **`A11Y`**

- **element** { [string](dataTypes#string) } - Element name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ move to previous element ] action](uiObjectActionsType#m-previoushtmlelement).

## [m#] showTextSuggestions

### showTextSuggestions()

**`6.2.0`** **`A11Y`** **`API>=33`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ show text suggestions ] action](uiObjectActionsType#m-showtextsuggestions).

## [m#] showTooltip

### showTooltip()

**`6.2.0`** **`A11Y`** **`API>=28`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ show tooltip information ] action](uiObjectActionsType#m-showtooltip).

## [m#] hideTooltip

### hideTooltip()

**`6.2.0`** **`A11Y`** **`API>=28`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ hide tooltip information ] action](uiObjectActionsType#m-hidetooltip).

## [m#] show

### show()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ show in viewport ] action](uiObjectActionsType#m-show).

## [m#] dismiss

### dismiss()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ dismiss ] action](uiObjectActionsType#m-dismiss).

## [m#] copy

### copy()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ copy text ] action](uiObjectActionsType#m-copy).

## [m#] cut

### cut()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ cut text ] action](uiObjectActionsType#m-cut).

## [m#] paste

### paste()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ paste text ] action](uiObjectActionsType#m-paste).

## [m#] select

### select()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ select ] action](uiObjectActionsType#m-select).

## [m#] expand

### expand()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ expand ] action](uiObjectActionsType#m-expand).

## [m#] collapse

### collapse()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ collapse ] action](uiObjectActionsType#m-collapse).

## [m#] scrollLeft

### scrollLeft()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ scroll to move viewport left ] action](uiObjectActionsType#m-scrollleft).

## [m#] scrollUp

### scrollUp()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ scroll to move viewport up ] action](uiObjectActionsType#m-scrollup).

## [m#] scrollRight

### scrollRight()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ scroll to move viewport right ] action](uiObjectActionsType#m-scrollright).

## [m#] scrollDown

### scrollDown()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ scroll to move viewport down ] action](uiObjectActionsType#m-scrolldown).

## [m#] scrollForward

### scrollForward()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ scroll to move viewport forward ] action](uiObjectActionsType#m-scrollforward).

## [m#] scrollBackward

### scrollBackward()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ scroll to move viewport backward ] action](uiObjectActionsType#m-scrollbackward).

## [m#] scrollTo

### scrollTo(row, column)

**`A11Y`**

- **row** { [number](dataTypes#number) } - Row ordinal
- **column** { [number](dataTypes#number) } - Column ordinal
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ scroll specified position into viewport ] action](uiObjectActionsType#m-scrollto).

## [m#] contextClick

### contextClick()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ context click ] action](uiObjectActionsType#m-contextclick).

## [m#] setText

### setText(text)

**`A11Y`**

- **text** { [string](dataTypes#string) } - Text
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ set text ] action](uiObjectActionsType#m-settext).

## [m#] setSelection

### setSelection(start, end)

**`A11Y`**

- **start** { [number](dataTypes#number) } - Start position
- **end** { [number](dataTypes#number) } - End position
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ select text ] action](uiObjectActionsType#m-setselection).

## [m#] clearSelection

### clearSelection()

**`6.2.0`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ clear text selection ] action](uiObjectActionsType#m-clearselection).

## [m#] setProgress

### setProgress(progress)

**`A11Y`**

- **progress** { [number](dataTypes#number) } - Progress value
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

The control node executes the [[ set progress value ] action](uiObjectActionsType#m-setprogress).

## [m#] compass

### compass(compassArg)

**`6.2.0`** **`A11Y`**

- **compassArg** { [DetectCompass](dataTypes#detectcompass) } - Compass argument, used to control compass positioning
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) } - The final positioned control node by the compass

Returns the final [control node](uiObjectType) positioned by the compass. Returns null if positioning fails.

Compass positioning is similar to freely moving within the [control hierarchy](glossaries#control-hierarchy), ultimately landing on a specific control node.

```js
let w = clickable().findOnce();

console.log(w.parent()); /* Parent control. */
console.log(w.parent().parent()); /* Second-level parent. */
console.log(w.child(0)); /* Index 0 (first) child. */
console.log(w.child(2)); /* Index 2 child. */
console.log(w.child(w.childCount() - 1)); /* Last child. */
console.log(w.parent().child(5)); /* Index 5 sibling. */
console.log(w.parent().child(w.childCount() - 2)); /* Second-to-last sibling. */
console.log(w.parent().child(w.indexInParent() - 1)); /* Left adjacent sibling. */
console.log(w.parent().child(w.indexInParent() + 1)); /* Right adjacent sibling. */
console.log(w.parent().parent().parent().parent().child(0).child(1).child(1).child(0)); /* Multi-level access. */

/* Replace all the above statements using the control compass. */

console.log(w.compass('p')); /* Parent control. */
console.log(w.compass('p2')); /* Second-level parent. */
console.log(w.compass('c0')); /* Index 0 (first) child. */
console.log(w.compass('c2')); /* Index 2 child. */
console.log(w.compass('c-1')); /* Last child. */
console.log(w.compass('s5')); /* Index 5 sibling. */
console.log(w.compass('s-2')); /* Second-to-last sibling. */
console.log(w.compass('s<1')); /* Left adjacent sibling. */
console.log(w.compass('s>1')); /* Right adjacent sibling. */
console.log(w.compass('p4c0>1>1>0')); /* Multi-level access. */
```

The compass arguments fall into the following categories:

- p: [parent](#parent-p)
- c: [child](#child-c)
- s: [sibling](#sibling-s)
- k: [clickable](#clickable-k)

Different types of compass arguments can be used repeatedly or combined.

#### parent (p)

Access the parent control.

Two compass positioning forms for `w.parent()`:

```js
w.compass('p'); /* Most commonly used. */
w.compass('p1');
```

The `p` compass can be followed by a number to indicate hierarchy span:

```js
/* Second level. */
w.parent().parent(); /* Original method. */
w.compass('pp');
w.compass('p2'); /* Most commonly used. */

/* Fifth level. */
w.parent().parent().parent().parent().parent(); /* Original method. */
w.compass('ppppp');
w.compass('p5'); /* Most commonly used. */
w.compass('p4p');
w.compass('p3p2');
w.compass('p2p1p2');
```

Each time the `p` compass moves, the control's depth decreases by one level. When depth reaches 0, all further parent accesses return null:

```js
console.log(w.depth()); /* e.g. 23 */
console.log(w.compass('p5').depth()); /* e.g. 18 */
console.log(w.compass('p23').depth()); /* e.g. 0 */
console.log(w.compass('p24')); // null
console.log(w.compass('p40')); // null
```

The `p` compass throws an exception when followed by a negative number:

```js
/* e.g. java.lang.IllegalArgumentException: Invalid remaining compass argument: -2 */
console.log(w.compass('p-2'));
```

`p0` returns the control itself:

```js
console.log(w.compass('p0') === w); // true
```

#### child (c)

Access child controls.

Compass positioning form for `w.child(0)`:

```js
w.compass('c0');
```

The `c` compass can be followed by an integer to indicate the child index:

```js
/* Index 2 child */
w.child(2);
w.compass('c2');

/* Second-to-last child. */
w.child(w.childCount() - 2);
w.compass('c-2');
```

For consecutive multi-level child access, use the `cXcYcZ` or `cX>Y>Z` form:

```js
w.child(1).child(1).child(0).child(5).child(2).child(3);
w.compass('c1c1c0c5c2c3');
w.compass('c1>1>0>5>2>3'); /* Same as above. */
```

#### sibling (s)

Access sibling controls.

For example, if a control has 10 child controls, these child controls are siblings to each other and share the same parent control.  
Among the 10 child controls, the one with index n (where n > 0 and n < 9) has two adjacent sibling nodes: the left sibling at index n-1 and the right sibling at index n+1.

```js
/* Left adjacent sibling node. */
w.parent().child(w.indexInParent() - 1);
w.compass('s<1');

/* Right adjacent sibling node. */
w.parent().child(w.indexInParent() + 1);
w.compass('s>1');

/* Second sibling to the right. */
w.parent().child(w.indexInParent() + 2);
w.compass('s>2');

/* Index 5 sibling. */
w.parent().child(5);
w.compass('s5');

/* Second-to-last sibling. */
w.parent().child(w.childCount() - 2);
w.compass('s-2');
```

#### clickable (k)

Access clickable controls.

Some controls are not clickable themselves but are contained inside a clickable control:

```js
let w = contentMatch(/.+/).findOnce();
console.log(w.clickable()); // false
console.log(w.parent().clickable()); // true
```

For such controls, performing "parentControl.click()" usually achieves the expected result — even though the parent is clicked, the actual effect is the same as clicking the control itself.

In some cases, such a clickable parent control may require two or more levels:

```js
let w = contentMatch(/.+/).findOnce();
console.log(w.clickable()); // false
console.log(w.parent().clickable()); // false
console.log(w.parent().parent().clickable()); // false
console.log(w.parent().parent().parent().clickable()); // false
console.log(w.parent().parent().parent().parent().clickable()); // true
```

In the example above, only the 4th-level parent is clickable. For such cases, a loop combined with the `clickable` condition check is usually needed:

```js
let w = contentMatch(/.+/).findOnce();
let max = 5;
let temp = w;
while (max--) {
    if (temp !== null && temp.clickable()) {
        temp.click();
        break;
    }
    temp = temp.parent();
}
```

The `max` variable in the example above represents the maximum number of levels to try. If too small, you might miss the actual clickable parent; if too large, you may get an unrelated clickable control (clicking it may produce unexpected results). Usually, setting `max` to 2 is recommended.

Expressing the above example using the control compass:

```js
let w = contentMatch(/.+/).findOnce();
let temp = w.compass('k5'); /* 5 indicates the maximum levels to try, usually recommended to set to 2. */
if (temp !== null && temp.clickable()) {
    temp.click();
}
```

Expressing the above example using a [pickup selector](uiSelectorType#m-pickup):

```js
pickup(/.+/, 'k5', 'click');
```

## [m] isCompass

### isCompass(s)

**`6.2.0`** **`A11Y`**

- **s** { [string](dataTypes#string) } - Compass argument
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Checks whether the compass argument conforms to the established format.

```js
console.log(UiObject.isCompass('p2c3')); // true
console.log(UiObject.isCompass('p-2c3')); // true
console.log(UiObject.isCompass('p2c-3')); // true
console.log(UiObject.isCompass('hello')); // false
```

In the example above, the `p-2c3` compass argument will throw an exception when used, but because it conforms to the established format, `isCompass` returns `true`.

## [m] ensureCompass

### ensureCompass(s)

**`6.2.0`** **`A11Y`**

- **s** { [string](dataTypes#string) } - Compass argument
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Ensures the compass argument conforms to the established format; throws an exception if it does not.

```js
UiObject.ensureCompass('p2c3'); /* No exception. */
UiObject.ensureCompass('world'); /* Throws exception. */
```

## [m] detect

Control detection.

Detection is equivalent to performing a series of combined operations on a control (compass positioning, result filtering, parameterized invocation, callback processing).

Some characteristics:

- `detect` has been globalized and supports global usage.
- The first parameter of `detect` is always of type [UiObject](uiObjectType).
- [compass](#m-compass) is a derived method of `detect`.
- The internal implementation of [pickup](uiSelectorType#m-pickup) references the `detect` method.

### detect(w, compass)

**`6.2.0`** **`Global`** **`Overload 1/7`** **`A11Y`**

- **w** { [UiObject](uiObjectType) } - Control node
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Compass argument
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) } - Detected control node

Control detection carrying a [compass argument](dataTypes#detectcompass).

Equivalent to [w.compass(compass)](#m-compass), therefore `compass` is a derived method of `detect`.

### detect(w, result)

**`6.2.0`** **`Global`** **`Overload 2/7`** **`A11Y`**

- **w** { [UiObject](uiObjectType) } - Control node
- **result** { [DetectResult](dataTypes#detectresult) } - Detection result argument
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) } - Detection result

Control detection carrying a [detection result argument](dataTypes#detectresult).

### detect(w, compass, result)

**`6.2.0`** **`Global`** **`Overload 3/7`** **`A11Y`**

- **w** { [UiObject](uiObjectType) } - Control node
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Compass argument
- **result** { [DetectResult](dataTypes#detectresult) } - Detection result argument
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) } - Detection result

Control detection carrying both a [compass argument](dataTypes#detectcompass) and a [detection result argument](dataTypes#detectresult).

Pay special attention to the order of compass and result. When both are strings, the first one is parsed as the `compass argument`.

```js
console.log(w.parent().parent().child(1).child(0).bounds()); /* Potential null-pointer exception. */
console.log(detect(w, 'p2c1>0', 'bounds')); /* Null-pointer safe. */
```

### detect(w, callback)

**`6.2.0`** **`Global`** **`Overload 4/7`** **`A11Y`**

- **w** { [UiObject](uiObjectType) } - Control node
- **callback** { [DetectCallback](dataTypes#detectcallback) } - Detection callback
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) } - Result of the detection callback

Control detection carrying a [detection callback](dataTypes#detectcallback).

```js
detect(pickup(/^[A-Z][a-z]+ ?\d*$/), (w) => {
    w ? w.click() : console.warn('Specified control not found');
});
```

### detect(w, compass, callback)

**`6.2.0`** **`Global`** **`Overload 5/7`** **`A11Y`**

- **w** { [UiObject](uiObjectType) } - Control node
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Compass argument
- **callback** { [DetectCallback](dataTypes#detectcallback) } - Detection callback
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) } - Result of the detection callback

Control detection carrying both a [compass argument](dataTypes#detectcompass) and a [detection callback](dataTypes#detectcallback).

```js
detect(pickup(/^[A-Z][a-z]+ ?\d*$/), 'k2', (w) => {
    w ? w.click() : console.warn('Specified control not found');
});
```

### detect(w, result, callback)

**`6.2.0`** **`Global`** **`Overload 6/7`** **`A11Y`**

- **w** { [UiObject](uiObjectType) } - Control node
- **result** { [DetectResult](dataTypes#detectresult) } - Detection result argument
- **callback** { [DetectCallback](dataTypes#detectcallback) } - Detection callback
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) } - Result of the detection callback

Control detection carrying both a [detection result argument](dataTypes#detectresult) and a [detection callback](dataTypes#detectcallback).

```js
detect(pickup(/^[A-Z][a-z]+ ?\d*$/), 'content', (content) => {
    content ? console.log(content) : console.warn('No text content or failed to locate the specified control');
});
```

### detect(w, compass, result, callback)

**`6.2.0`** **`Global`** **`Overload 7/7`** **`A11Y`**

- **w** { [UiObject](uiObjectType) } - Control node
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Compass argument
- **result** { [DetectResult](dataTypes#detectresult) } - Detection result argument
- **callback** { [DetectCallback](dataTypes#detectcallback) } - Detection callback
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) } - Result of the detection callback

Control detection carrying a [compass argument](dataTypes#detectcompass), a [detection result argument](dataTypes#detectresult), and a [detection callback](dataTypes#detectcallback).

Pay special attention to the order of compass and result. When both are strings, the first one is parsed as the `compass argument`.

```js
detect(pickup({ clickable: true }), 'p2c1', 'content', (content) => {
    content ? console.log(content) : console.warn('No text content or failed to locate the specified control');
});
```