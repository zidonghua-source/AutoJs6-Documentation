# Selector (UiSelector)

`UiSelector` (selector) can also be viewed as a condition filter for [control nodes](uiObjectType). It is used to filter one or more `control nodes` from the active window(s) by attaching different conditions, and then perform further processing, such as [ executing [control actions](uiObjectActionsType) (click, long click, set text, etc.) / determining position / retrieving text content / getting specific control states / performing [compass](uiObjectType#m-compass) navigation within the [control hierarchy](glossaries#control-hierarchy) ], etc.

```js
text("Start immediately");
```

The example above is a selector that requires the control to satisfy the condition where its text is "Start immediately".

Selectors are usually built based on control properties, such as [text / desc / className / action / height / id], etc.

After calling a builder-style selector method, it returns the same type, allowing the use of [method chaining](https://en.wikipedia.org/wiki/Method_chaining) to build selectors for multi-condition filtering:

```js
text("Start immediately").minHeight(0.2).clickable(true);
```

The example above is a multi-condition selector that requires the control to satisfy three conditions simultaneously: text is "Start immediately", height is at least 20% of the screen height, and the control is clickable. See the [Chaining Characteristics](#chaining-characteristics) section in this chapter for details.

In this chapter, the return type of most methods is annotated as "UiSelector". These are "selector builder methods" that support chaining. Other methods are collectively called "actions" and can be categorized as "state methods" (actions that check state), "find methods" (actions that find controls), and "[action methods](uiObjectActionsType)" (actions that perform control behaviors).

Selector builder methods:

- [m#] text
- [m#] desc
- [m#] id
- [m#] className
- ... ...

State methods:

- [m#] exists
- [m#] toString

Find methods:

- [m#] findOnce
- [m#] find
- [m#] findOne
- [m#] untilFindOne
- [m#] untilFind / waitFor
- [m] pickup

Action methods:

- [m#] click
- [m#] longClick
- [m#] focus
- [m#] clearFocus
- ... ...

Once a selector is built, one of the above "actions" must be executed for the selector to take effect:

```js
let sel = text("Start immediately").minHeight(0.2).clickable(true);
console.log(sel.exists()); /* State-checking action. */
console.log(sel.findOnce()); /* Control-finding action. */
console.log(sel.click()); /* Control behavior action. */
```

---

<p style="font: bold 2em sans-serif; color: #FF7043">UiSelector</p>

---

## [@] UiSelector

**`Global`**

To build a UiSelector, you can use any of the "selector builder methods" in this chapter, and they are all globally available:

```js
console.log(text("Start immediately") instanceof UiSelector); // true
console.log(text("Start immediately").clickable() instanceof UiSelector); // true
```

To build an "empty" selector, you can use the `selector` method:

```js
console.log(selector()); // class org.autojs.autojs.core.automator.filter.Selector
console.log(selector() instanceof UiSelector); // true
```

When a selector name conflicts with a user-defined variable name in the current scope, you can use the `selector` method to avoid the conflict:

```js
/* The text selector is overwritten. */
let text = "hello";

/* text is no longer a selector. */
console.log(text("Start immediately").exists()); // TypeError: text is a string, not a function.

/* Use selector() to avoid naming conflicts. */
console.log(selector().text("Start immediately").exists()); // e.g. true
```

## [m#] id

### id(str)

**`[6.2.0]`** **`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

ID resource selector.

- Filtering condition: The full ID resource name or the ID resource entry name exactly matches the specified string.
- Associated control property: [id](uiObjectType#m-id)

The full Android resource name format is `package:type/entry`, i.e., `package:type/resource_entry`.  
The `type` of a full ID resource name is `id`.  
An example of a valid full ID resource name: `com.test:id/some_entry`.  
Here, `com.test` is the package name, `some_entry` is the ID resource entry name, and `com.test:id/some_entry` is the full ID resource name.

In AutoJs6, the ID resource selector supports two ways to specify the filtering condition:

- Full ID resource name (corresponding to `com.test:id/some_entry` in the example above)
- ID resource entry name (corresponding to `some_entry` in the example above)

For example, for the following 4 controls:

```js
wA.id(); // com.test.abc:id/some_entry
wB.id(); // com.test.abc:id/some_other_entry
wC.id(); // com.test.jkl:id/some_entry
wD.id(); // com.test.xyz:id/some_entry
```

`id('com.test.abc:id/some_entry')` is a full ID resource name selector and will match control `wA`.

`id('com.test.xyz:id/some_entry')` is also a full ID resource name selector and will match control `wD`.

`id('some_entry')` is an ID resource entry name selector.  
It does not contain package name information and only cares about the resource entry name during matching. Therefore, `wA`, `wC`, and `wD` can all be matched.  
Note that this matching behavior differs from Auto.js 4.x versions, where the package name of the foreground activity was considered during filtering.  
If your code needs to be compatible with different Auto.js versions, it is recommended to use [idEndsWith](#m-idendswith) (e.g., `idEndsWith('some_entry')`) or [idMatches](#m-idmatches) (e.g., `idMatches(/.*some_entry/)`).

[Pickup selector](#m-pickup) examples:

```js
pickup(id('some_entry'), '@');
pickup({ id: 'some_entry' }, '@');
pickup({ id: [ 'some_entry' ] }, '@');
```

> Method change log
> - 6.2.0 - When the filtering condition is an ID resource entry (not the full ID resource name), package name matching is ignored.

## [m#] idStartsWith

### idStartsWith(str)

**`[6.2.0]`** **`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Prefix matching filter for the [ID resource selector](#m-id).

- Filtering condition: The full ID resource name prefix or the ID resource entry name prefix matches the specified string.
- Associated control property: [id](uiObjectType#m-id)

In AutoJs6, the ID resource prefix matching selector supports two ways to specify the filtering condition:

- Full ID resource name (e.g., `com.test:id/some_entry`)
- ID resource entry name (e.g., `some_entry`)

For example, for the following 4 controls:

```js
wA.id(); // com.test.abc:id/some_entry
wB.id(); // com.test.abc:id/some_other_entry
wC.id(); // com.test.jkl:id/some_entry
wD.id(); // com.test.xyz:id/some_entry
```

`idStartsWith('com.test.abc:id/some_')` is an ID prefix matching selector that includes the package name and will match controls `wA` and `wB`.

`idStartsWith('com.test.xyz:id/some_')` is also an ID prefix matching selector that includes the package name and will match control `wD`.

`idStartsWith('some_')` is a prefix matching selector that only contains the ID resource entry name.  
It does not include package name information and only cares about the resource entry name during matching. Therefore, `wA`, `wB`, `wC`, and `wD` can all be matched.  
Note that this matching behavior differs from Auto.js 4.x versions, where the package name of the foreground activity was considered during filtering.  
If your code needs to be compatible with different Auto.js versions, it is recommended to use [idMatches](#m-idmatches) (e.g., `idMatches(/.*some_.*/)`).

[Pickup selector](#m-pickup) examples:

```js
pickup(idStartsWith('some_'), '@');
pickup({ idStartsWith: 'some_' }, '@');
pickup({ idStartsWith: [ 'some_' ] }, '@');
```

> Method change log
> - 6.2.0 - When the filtering condition is an ID resource entry (not the full ID resource name), package name matching is ignored.

## [m#] idEndsWith

### idEndsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Suffix matching filter for the [ID resource selector](#m-id).

- Filtering condition: The full ID resource name suffix matches the specified string.
- Associated control property: [id](uiObjectType#m-id)

For example, for the following 4 controls:

```js
wA.id(); // com.test.abc:id/some_entry
wB.id(); // com.test.abc:id/some_other_entry
wC.id(); // com.test.jkl:id/some_entry
wD.id(); // com.test.xyz:id/some_entry
```

`idEndsWith('abc')` will not match any of the above controls.

`idEndsWith('some_entry')` will match controls `wA`, `wC`, and `wD`.

`idEndsWith('_entry')` will match controls `wA`, `wB`, `wC`, and `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(idEndsWith('_entry'), '@');
pickup({ idEndsWith: '_entry' }, '@');
pickup({ idEndsWith: [ '_entry' ] }, '@');
```

## [m#] idContains

### idContains(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Contains matching filter for the [ID resource selector](#m-id).

- Filtering condition: Any length of consecutive characters in the full ID resource name matches the specified string.
- Associated control property: [id](uiObjectType#m-id)

The ID resource contains matching selector performs matching against both the `full ID resource name` and the `ID resource entry name`.

For example, for the following 4 controls:

```js
wA.id(); // com.test.abc:id/some_entry
wB.id(); // com.test.abc:id/some_other_entry
wC.id(); // com.test.jkl:id/some_entry
wD.id(); // com.test.xyz:id/some_entry
```

`idContains('abc')` will match controls `wA` and `wB` because `'abc'` matches their ID resource package name.

`idContains('com.test.')` will match controls `wA`, `wB`, `wC`, and `wD` because `'com.test.'` matches their ID resource package name.

`idContains('other')` will match control `wB` because `'other'` matches its ID resource entry name.

`idContains('some_')` will match controls `wA`, `wB`, `wC`, and `wD` because `'some_'` matches their ID resource entry name.

[Pickup selector](#m-pickup) examples:

```js
pickup(idContains('some_'), '@');
pickup({ idContains: 'some_' }, '@');
pickup({ idContains: [ 'some_' ] }, '@');
```

## [m#] idMatches

### idMatches(regex)

**`Global`** **`DEPRECATED`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression full match filter for the [ID resource selector](#m-id).

- Filtering condition: The full ID resource name's regular expression rule exactly matches the specified parameter.
- Associated control property: [id](uiObjectType#m-id)

The ID regular expression full match selector performs matching against both the `full ID resource name` and the `ID resource entry name`.

For example, for the following 4 controls:

```js
wA.id(); // com.test.abc:id/some_entry
wB.id(); // com.test.abc:id/some_other_entry
wC.id(); // com.test.jkl:id/some_entry
wD.id(); // com.test.xyz:id/some_entry
```

`idMatches(/abc/)` or `idMatches('abc')` cannot match any of the above controls (because `idMatches(/abc/)` is equivalent to `idMatch(/^abc$/)`).

`idMatches(/com\.test\..+/)` or `idMatches('com\\.test\\..+')` can match controls `wA`, `wB`, `wC`, and `wD`, because `/^com\.test\..+$/` matches their ID resource package names.

`idMatches(/other/)` or `idMatches('other')` cannot match any of the above controls.

`idMatches(/.*other.*/)` or `idMatches('.*other.*')` can match control `wB`, because `/^.*other.*$/` matches its ID resource entry name.

`idMatches(/some_/)` or `idMatches('some_')` cannot match any of the above controls.

`idMatches(/.*some_.*/)` or `idMatches('.*some_.*')` can match controls `wA`, `wB`, `wC`, and `wD`, because `/^.*some_.*$/` matches their ID resource entry names.

[Pickup selector](#m-pickup) examples:

```js
pickup(idMatches(/.*some_.*/), '@');
pickup({ idMatches: /.*some_.*/ }, '@');
pickup({ idMatches: [ /.*some_.*/ ] }, '@');
```

> Note: Since version 6.2.0, idMatches has been deprecated. It is recommended to use [idMatch](#m-idmatch). See the [Regular Expression Full Match Filter](#xxxmatches) section for details.

## [m#] idMatch

### idMatch(regex)

**`6.2.0`** **`Global`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression match filter for the [ID resource selector](#m-id).

- Filtering condition: The regular expression rule of the full ID resource name matches the specified parameter.
- Associated control property: [id](uiObjectType#m-id)

The ID regular expression match selector performs matching against both the `full ID resource name` and the `ID resource entry name`.

For example, for the following 4 controls:

```js
wA.id(); // com.test.abc:id/some_entry
wB.id(); // com.test.abc:id/some_other_entry
wC.id(); // com.test.jkl:id/some_entry
wD.id(); // com.test.xyz:id/some_entry
```

`idMatch(/abc/)` or `idMatch('abc')` will match controls `wA` and `wB` because `/abc/` matches their ID resource package name.

`idMatch(/com\.test\..+/)` or `idMatch('com\\.test\\..+')` will match controls `wA`, `wB`, `wC`, and `wD` because `/com\.test\..+/` matches their ID resource package name.

`idMatch(/other/)` or `idMatch('other')` will match control `wB` because `/other/` matches its ID resource entry name.

`idMatch(/some_/)` or `idMatch('some_')` will match controls `wA`, `wB`, `wC`, and `wD` because `/some_/` matches their ID resource entry name.

[Pickup selector](#m-pickup) examples:

```js
pickup(idMatch(/some_/), '@');
pickup({ idMatch: /some_/ }, '@');
pickup({ idMatch: [ /some_/ ] }, '@');
```

## [m#] text

### text(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Text exact match selector.

- Filtering condition: The control's `text` property exactly matches the specified string.
- Associated control property: [text](uiObjectType#m-text)

This is one of the most commonly used selectors.

```js
text("Start immediately");
```

## [m#] textStartsWith

### textStartsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Text prefix match selector.

- Filtering condition: The control's `text` property starts with the specified string.
- Associated control property: [text](uiObjectType#m-text)

## [m#] textEndsWith

### textEndsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Text suffix match selector.

- Filtering condition: The control's `text` property ends with the specified string.
- Associated control property: [text](uiObjectType#m-text)

## [m#] textContains

### textContains(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Text contains match selector.

- Filtering condition: The control's `text` property contains the specified string.
- Associated control property: [text](uiObjectType#m-text)

**`6.2.0`** **`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

ID resource hexadecimal value selector.

```js
console.log(idHex('0x7f090117').findOnce().idEntry()); /* e.g. explorer_item_list */
```

## [m#] text

### text(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Text exact match selector.

- Filtering condition: The control's text exactly matches the specified string.
- Associated control property: [text](uiObjectType#m-text)

For example, for the following 4 controls:

```js
wA.text(); // start
wB.text(); // Service Notification
wC.text(); // Contacts
wD.text(); // Coconuts
```

`text('Coconuts')` is a text selector that will match control `wD`.

`text('start')` is also a text selector that will match control `wA`.  
However, `text('START')` will not match any of the above controls because text matching is case-sensitive.

[Pickup selector](#m-pickup) examples:

```js
pickup(text('start'), '@');
pickup({ text: 'start' }, '@');
pickup({ text: [ 'start' ] }, '@');
```

## [m#] textStartsWith

### textStartsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Prefix matching filter for the [text selector](#m-text).

- Filtering condition: The text prefix matches the specified string.
- Associated control property: [text](uiObjectType#m-text)

For example, for the following 4 controls:

```js
wA.text(); // start
wB.text(); // Service Notification
wC.text(); // Contacts
wD.text(); // Coconuts
```

`textStartsWith('Co')` is a text selector that will match controls `wC` and `wD`.

`textStartsWith('star')` is also a text selector that will match control `wA`. Note that text matching is case-sensitive.

[Pickup selector](#m-pickup) examples:

```js
pickup(textStartsWith('star'), '@');
pickup({ textStartsWith: 'star' }, '@');
pickup({ textStartsWith: [ 'star' ] }, '@');
```

## [m#] textEndsWith

### textEndsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Suffix matching filter for the [text selector](#m-text).

- Filtering condition: The text suffix matches the specified string.
- Associated control property: [text](uiObjectType#m-text)

For example, for the following 4 controls:

```js
wA.text(); // start
wB.text(); // Service Notification
wC.text(); // Contacts
wD.text(); // Coconuts
```

`textEndsWith('vice')` will not match any of the above controls.

`textEndsWith('ts')` will match controls `wC` and `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(textEndsWith('ts'), '@');
pickup({ textEndsWith: 'ts' }, '@');
pickup({ textEndsWith: [ 'ts' ] }, '@');
```

## [m#] textContains

### textContains(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Contains matching filter for the [text selector](#m-text).

- Filtering condition: Any length of consecutive characters in the text matches the specified string.
- Associated control property: [text](uiObjectType#m-text)

For example, for the following 4 controls:

```js
wA.text(); // start
wB.text(); // Service Notification
wC.text(); // Contacts
wD.text(); // Coconuts
```

`textContains('t')` will match controls `wA`, `wB`, `wC`, and `wD`.

`textContains('on')` will match controls `wB` and `wC`.

[Pickup selector](#m-pickup) examples:

```js
pickup(textContains('on'), '@');
pickup({ textContains: 'on' }, '@');
pickup({ textContains: [ 'on' ] }, '@');
```

## [m#] textMatches

### textMatches(regex)

**`Global`** **`DEPRECATED`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression full match filter for the [text selector](#m-text).

- Filtering condition: The regular expression rule of the control's `text` property fully matches the specified parameter.
- Associated control property: [text](uiObjectType#m-text)

For example, for the following 4 controls:

```js
wA.text(); // start
wB.text(); // Service Notification
wC.text(); // Contacts
wD.text(); // Coconuts
```

`textMatches(/star/)` or `textMatches('star')` will not match any of the above controls (because `textMatches(/star/)` is equivalent to `textMatch(/^star$/)`).

`textMatches(/Co\w+ts/)` or `textMatches('Co\\w+ts')` will match controls `wC` and `wD` because `/^Co\w+ts$/` matches their text.

`textMatches(/cat/)` or `textMatches('cat')` will not match any of the above controls.

`textMatches(/.*cat.*/)` or `textMatches('.*cat.*')` will match control `wB` because `/^.*cat.*$/` matches its text.

`textMatches(/t\w{0,3}/)` or `textMatches('t\\w{0,3}')` will not match any of the above controls.

`textMatches(/.*t\w{0,3}/)` or `textMatches('.*t\\w{0,3}')` will match controls `wA`, `wB`, `wC`, and `wD` because `/^.*t\w{0,3}$/` matches their text.

[Pickup selector](#m-pickup) examples:

```js
pickup(textMatches(/.*t\w{0,3}/), '@');
pickup({ textMatches: /.*t\w{0,3}/ }, '@');
pickup({ textMatches: [ /.*t\w{0,3}/ ] }, '@');
```

> Note: Since version 6.2.0, textMatches has been deprecated. It is recommended to use [textMatch](#m-textmatch). See the [Regular Expression Full Match Filter](#xxxmatches) section for details.

## [m#] textMatch

### textMatch(regex)

**`6.2.0`** **`Global`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression match filter for the [text selector](#m-text).

- Filtering condition: The regular expression rule of the text matches the specified parameter.
- Associated control property: [text](uiObjectType#m-text)

For example, for the following 4 controls:

```js
wA.text(); // start
wB.text(); // Service Notification
wC.text(); // Contacts
wD.text(); // Coconuts
```

`textMatch(/star/)` or `textMatch('star')` will match control `wA`.

`textMatch(/Co\w+ts/)` or `textMatch('Co\\w+ts')` will match controls `wC` and `wD`.

`textMatch(/cat/)` or `textMatch('cat')` will match control `wB`.

`textMatch(/t\w{0,3}/)` or `textMatch('t\\w{0,3}')` will match controls `wA`, `wB`, `wC`, and `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(textMatch(/t\w{0,3}/), '@');
pickup({ textMatch: /t\w{0,3}/ }, '@');
pickup({ textMatch: [ /t\w{0,3}/ ] }, '@');
```

## [m#] desc

### desc(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Content description (desc) exact match selector.

- Filtering condition: The content description exactly matches the specified string.
- Associated control property: [desc](uiObjectType#m-desc)

For example, for the following 4 controls:

```js
wA.desc(); // start
wB.desc(); // Service Notification
wC.desc(); // Contacts
wD.desc(); // Coconuts
```

`desc('Coconuts')` is a content description selector that will match control `wD`.

`desc('start')` is also a content description selector that will match control `wA`.  
However, `desc('START')` will not match any of the above controls because content description matching is case-sensitive.

[Pickup selector](#m-pickup) examples:

```js
pickup(desc('start'), '@');
pickup({ desc: 'start' }, '@');
pickup({ desc: [ 'start' ] }, '@');
```

## [m#] descStartsWith

### descStartsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Prefix matching filter for the [content description selector](#m-desc).

- Filtering condition: The content description prefix matches the specified string.
- Associated control property: [desc](uiObjectType#m-desc)

For example, for the following 4 controls:

```js
wA.desc(); // start
wB.desc(); // Service Notification
wC.desc(); // Contacts
wD.desc(); // Coconuts
```

`descStartsWith('Co')` is a content description selector that will match controls `wC` and `wD`.

`descStartsWith('star')` is also a content description selector that will match control `wA`. Note that content description matching is case-sensitive.

[Pickup selector](#m-pickup) examples:

```js
pickup(descStartsWith('star'), '@');
pickup({ descStartsWith: 'star' }, '@');
pickup({ descStartsWith: [ 'star' ] }, '@');
```

## [m#] descEndsWith

### descEndsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Suffix matching filter for the [content description selector](#m-desc).

- Filtering condition: The content description suffix matches the specified string.
- Associated control property: [desc](uiObjectType#m-desc)

For example, for the following 4 controls:

```js
wA.desc(); // start
wB.desc(); // Service Notification
wC.desc(); // Contacts
wD.desc(); // Coconuts
```

`descEndsWith('vice')` will not match any of the above controls.

`descEndsWith('ts')` will match controls `wC` and `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(descEndsWith('ts'), '@');
pickup({ descEndsWith: 'ts' }, '@');
pickup({ descEndsWith: [ 'ts' ] }, '@');
```

## [m#] descContains

### descContains(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Contains matching filter for the [content description selector](#m-desc).

- Filtering condition: The control's `desc` (content description) property matches the specified string for any length of consecutive characters.
- Associated control property: [desc](uiObjectType#m-desc)

For example, for the following 4 controls:

```js
wA.desc(); // start
wB.desc(); // Service Notification
wC.desc(); // Contacts
wD.desc(); // Coconuts
```

`descContains('t')` can match controls `wA`, `wB`, `wC`, and `wD`.

`descContains('on')` can match controls `wB` and `wC`.

[Pickup selector](#m-pickup) examples:

```js
pickup(descContains('on'), '@');
pickup({ descContains: 'on' }, '@');
pickup({ descContains: [ 'on' ] }, '@');
```

## [m#] descMatches

### descMatches(regex)

**`Global`** **`DEPRECATED`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression full match filter for the [content description selector](#m-desc).

- Filtering condition: The regular expression rule of the control's `desc` (content description) property fully matches the specified parameter.
- Associated control property: [desc](uiObjectType#m-desc)

For example, for the following 4 controls:

```js
wA.desc(); // start
wB.desc(); // Service Notification
wC.desc(); // Contacts
wD.desc(); // Coconuts
```

`descMatches(/star/)` or `descMatches('star')` will not match any of the above controls (because `descMatches(/star/)` is equivalent to `descMatch(/^star$/)`).

`descMatches(/Co\w+ts/)` or `descMatches('Co\\w+ts')` can match controls `wC` and `wD`, because `/^Co\w+ts$/` matches their content description labels.

`descMatches(/cat/)` or `descMatches('cat')` will not match any of the above controls.

`descMatches(/.*cat.*/)` or `descMatches('.*cat.*')` can match control `wB`, because `/^.*cat.*$/` matches its content description label.

`descMatches(/t\w{0,3}/)` or `descMatches('t\\w{0,3}')` will not match any of the above controls.

`descMatches(/.*t\w{0,3}/)` or `descMatches('.*t\\w{0,3}')` can match controls `wA`, `wB`, `wC`, and `wD`, because `/^.*t\w{0,3}$/` matches their content description labels.

[Pickup selector](#m-pickup) examples:

```js
pickup(descMatches(/.*t\w{0,3}/), '@');
pickup({ descMatches: /.*t\w{0,3}/ }, '@');
pickup({ descMatches: [ /.*t\w{0,3}/ ] }, '@');
```

> Note: Since version 6.2.0, descMatches has been deprecated. It is recommended to use [descMatch](#m-descmatch). See the [Regular Expression Full Match Filter](#xxxmatches) section for details.

## [m#] descMatch

### descMatch(regex)

**`6.2.0`** **`Global`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression match filter for the [content description selector](#m-desc).

- Filtering condition: The regular expression rule of the control's `desc` (content description) property matches the specified parameter.
- Associated control property: [desc](uiObjectType#m-desc)

For example, for the following 4 controls:

```js
wA.desc(); // start
wB.desc(); // Service Notification
wC.desc(); // Contacts
wD.desc(); // Coconuts
```

`descMatch(/star/)` or `descMatch('star')` can match control `wA`.

`descMatch(/Co\w+ts/)` or `descMatch('Co\\w+ts')` can match controls `wC` and `wD`.

`descMatch(/cat/)` or `descMatch('cat')` can match control `wB`.

`descMatch(/t\w{0,3}/)` or `descMatch('t\\w{0,3}')` can match controls `wA`, `wB`, `wC`, and `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(descMatch(/t\w{0,3}/), '@');
pickup({ descMatch: /t\w{0,3}/ }, '@');
pickup({ descMatch: [ /t\w{0,3}/ ] }, '@');
```

## [m#] content

### content(str)

**`6.2.0`** **`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Content exact match selector.

- Filtering condition: The control's `content` property exactly matches the specified string.
- Associated control property: [content](uiObjectType#m-content)

For example, for the following 4 controls:

```js
wA.content(); // start
wB.content(); // Service Notification
wC.content(); // Contacts
wD.content(); // Coconuts
```

`content('Coconuts')` is a content selector that can match control `wD`.

`content('start')` is also a content selector that can match control `wA`.  
However, `content('START')` cannot match any of the above controls, because content matching is case-sensitive.

[Pickup selector](#m-pickup) examples:

```js
pickup(content('start'), '@');
pickup({ content: 'start' }, '@');
pickup({ content: [ 'start' ] }, '@');
```

## [m#] contentStartsWith

### contentStartsWith(str)

**`6.2.0`** **`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Prefix match filter for the [content selector](#m-content).

- Filtering condition: The control's `content` property starts with the specified string.
- Associated control property: [content](uiObjectType#m-content)

For example, for the following 4 controls:

```js
wA.content(); // start
wB.content(); // Service Notification
wC.content(); // Contacts
wD.content(); // Coconuts
```

`contentStartsWith('Co')` is a content selector that can match controls `wC` and `wD`.

`contentStartsWith('star')` is also a content selector that can match control `wA`. Note that content matching is case-sensitive.

[Pickup selector](#m-pickup) examples:

```js
pickup(contentStartsWith('star'), '@');
pickup({ contentStartsWith: 'star' }, '@');
pickup({ contentStartsWith: [ 'star' ] }, '@');
```

## [m#] contentEndsWith

### contentEndsWith(str)

**`6.2.0`** **`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Suffix match filter for the [content selector](#m-content).

- Filtering condition: The control's `content` property ends with the specified string.
- Associated control property: [content](uiObjectType#m-content)

For example, for the following 4 controls:

```js
wA.content(); // start
wB.content(); // Service Notification
wC.content(); // Contacts
wD.content(); // Coconuts
```

`contentEndsWith('vice')` will not match any of the above controls.

`contentEndsWith('ts')` can match controls `wC` and `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(contentEndsWith('ts'), '@');
pickup({ contentEndsWith: 'ts' }, '@');
pickup({ contentEndsWith: [ 'ts' ] }, '@');
```

## [m#] contentContains

### contentContains(str)

**`6.2.0`** **`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Contains match filter for the [content selector](#m-content).

- Filtering condition: The control's `content` property matches the specified string for any length of consecutive characters.
- Associated control property: [content](uiObjectType#m-content)

For example, for the following 4 controls:

```js
wA.content(); // start
wB.content(); // Service Notification
wC.content(); // Contacts
wD.content(); // Coconuts
```

`contentContains('t')` can match controls `wA`, `wB`, `wC`, and `wD`.

`contentContains('on')` can match controls `wB` and `wC`.

[Pickup selector](#m-pickup) examples:

```js
pickup(contentContains('on'), '@');
pickup({ contentContains: 'on' }, '@');
pickup({ contentContains: [ 'on' ] }, '@');
```

## [m#] contentMatches

### contentMatches(regex)

**`6.2.0`** **`Global`** **`DEPRECATED`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression full match filter for the [content selector](#m-content).

- Filtering condition: The regular expression rule of the control's `content` property fully matches the specified parameter.
- Associated control property: [content](uiObjectType#m-content)

For example, for the following 4 controls:

```js
wA.content(); // start
wB.content(); // Service Notification
wC.content(); // Contacts
wD.content(); // Coconuts
```

`contentMatches(/star/)` or `contentMatches('star')` will not match any of the above controls (because `contentMatches(/star/)` is equivalent to `contentMatch(/^star$/)`).

`contentMatches(/Co\w+ts/)` or `contentMatches('Co\\w+ts')` can match controls `wC` and `wD`, because `/^Co\w+ts$/` matches their content.

`contentMatches(/cat/)` or `contentMatches('cat')` will not match any of the above controls.

`contentMatches(/.*cat.*/)` or `contentMatches('.*cat.*')` can match control `wB`, because `/^.*cat.*$/` matches its content.

`contentMatches(/t\w{0,3}/)` or `contentMatches('t\\w{0,3}')` will not match any of the above controls.

`contentMatches(/.*t\w{0,3}/)` or `contentMatches('.*t\\w{0,3}')` can match controls `wA`, `wB`, `wC`, and `wD`, because `/^.*t\w{0,3}$/` matches their content.

[Pickup selector](#m-pickup) examples:

```js
pickup(contentMatches(/.*t\w{0,3}/), '@');
pickup({ contentMatches: /.*t\w{0,3}/ }, '@');
pickup({ contentMatches: [ /.*t\w{0,3}/ ] }, '@');
```

> Note: Since version 6.2.0, contentMatches has been deprecated. It is recommended to use [contentMatch](#m-contentmatch). See the [Regular Expression Full Match Filter](#xxxmatches) section for details.

## [m#] contentMatch

### contentMatch(regex)

**`6.2.0`** **`Global`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression match filter for the [content selector](#m-content).

- Filtering condition: The regular expression rule of the control's `content` property matches the specified parameter.
- Associated control property: [content](uiObjectType#m-content)

For example, for the following 4 controls:

```js
wA.content(); // start
wB.content(); // Service Notification
wC.content(); // Contacts
wD.content(); // Coconuts
```

`contentMatch(/star/)` or `contentMatch('star')` can match control `wA`.

`contentMatch(/Co\w+ts/)` or `contentMatch('Co\\w+ts')` can match controls `wC` and `wD`.

`contentMatch(/cat/)` or `contentMatch('cat')` can match control `wB`.

`contentMatch(/t\w{0,3}/)` or `contentMatch('t\\w{0,3}')` can match controls `wA`, `wB`, `wC`, and `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(contentMatch(/t\w{0,3}/), '@');
pickup({ contentMatch: /t\w{0,3}/ }, '@');
pickup({ contentMatch: [ /t\w{0,3}/ ] }, '@');
```

## [m#] className

### className(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Class name exact match selector.

- Filtering condition: The control's `className` (or Android control class name shorthand) exactly matches the specified string.
- Associated control property: [className](uiObjectType#m-classname)

In AutoJs6, the class name selector supports two forms as filtering conditions:

- Full class name (e.g. `android.widget.EditText`)
- Android control class name shorthand (e.g. `EditText`)

For example, for the following 4 controls:

```js
wA.className(); // android.view.View
wB.className(); // android.widget.Button
wC.className(); // android.widget.EditText
wD.className(); // androidx.recyclerview.widget.RecyclerView
```

`className('android.widget.Button')` is a class name selector that can match control `wB`.  
`className('Button')` has the same effect as the above selector; it uses the Android control class name shorthand as the filtering condition.

`className('androidx.recyclerview.widget.RecyclerView')` is also a class name selector that can match control `wD`.  
However, `className('RecyclerView')` cannot match any of the above controls, because only class names starting with `android.widget.` can use the shorthand form for matching.

[Pickup selector](#m-pickup) examples:

```js
pickup(className('Button'), '@');
pickup({ className: 'Button' }, '@');
pickup({ className: [ 'Button' ] }, '@');
```

## [m#] classNameStartsWith

### classNameStartsWith(str)

**`[6.2.0]`** **`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Prefix match filter for the [class name selector](#m-classname).

- Filtering condition: The control's `className` starts with the specified string.
- Associated control property: [className](uiObjectType#m-classname)

In AutoJs6, the class name prefix match filter supports two forms as filtering conditions:

- Full class name (e.g. `android.widget.EditText`)
- Android control class name shorthand (e.g. `EditText`)

For example, for the following 4 controls:

```js
wA.className(); // android.view.View
wB.className(); // android.widget.Button
wC.className(); // android.widget.EditText
wD.className(); // androidx.recyclerview.widget.RecyclerView
```

`classNameStartsWith('android.widget.Bu')` is a class name prefix selector that can match control `wB`.  
`classNameStartsWith('Bu')` has the same effect as the above selector; it uses the Android control class name shorthand as the filtering condition.

`classNameStartsWith('androidx.recyclerview.widget.Rec')` is also a class name prefix selector that can match control `wD`.  
However, `classNameStartsWith('Rec')` cannot match any of the above controls, because only class names starting with `android.widget.` can use the shorthand form for prefix matching.

Note that the above matching behavior differs from Auto.js 4.x versions. In 4.x, shorthand forms were not supported for class name prefix matching.  
If your code needs to be compatible with different Auto.js versions, it is recommended to use [classNameEndsWith](#m-classnameendswith) (e.g. `classNameEndsWith('RecyclerView')`) or [classNameMatches](#m-classnamematches) (e.g. `classNameMatches(/.*Rec.*/)`).

[Pickup selector](#m-pickup) examples:

```js
pickup(classNameStartsWith('Rec'), '@');
pickup({ classNameStartsWith: 'Rec' }, '@');
pickup({ classNameStartsWith: [ 'Rec' ] }, '@');
```

> Method change record
> - 6.2.0 - Support Android control class name abbreviations as class name prefix filter conditions.

## [m#] classNameEndsWith

### classNameEndsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Suffix match filter for the [class name selector](#m-classname).

- Filtering condition: The control's `className` ends with the specified string.
- Associated control property: [className](uiObjectType#m-classname)

For example, for the following 4 controls:

```js
wA.className(); // android.view.View
wB.className(); // android.widget.Button
wC.className(); // android.widget.EditText
wD.className(); // androidx.recyclerview.widget.RecyclerView
```

`classNameEndsWith('View')` can match controls `wA` and `wD`.  
However, `classNameEndsWith('view')` cannot match any of the above controls, because class name matching is case-sensitive.

`classNameEndsWith('Button')` can match control `wB`.

[Pickup selector](#m-pickup) examples:

```js
pickup(classNameEndsWith('Button'), '@');
pickup({ classNameEndsWith: 'Button' }, '@');
pickup({ classNameEndsWith: [ 'Button' ] }, '@');
```

## [m#] classNameContains

### classNameContains(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Contains match filter for the [class name selector](#m-classname).

- Filtering condition: The control's `className` matches the specified string for any length of consecutive characters.
- Associated control property: [className](uiObjectType#m-classname)

For example, for the following 4 controls:

```js
wA.className(); // android.view.View
wB.className(); // android.widget.Button
wC.className(); // android.widget.EditText
wD.className(); // androidx.recyclerview.widget.RecyclerView
```

`classNameContains('android')` can match controls `wA`, `wB`, `wC`, and `wD`.

`classNameContains('Button')` can match control `wB`.

[Pickup selector](#m-pickup) examples:

```js
pickup(classNameContains('Button'), '@');
pickup({ classNameContains: 'Button' }, '@');
pickup({ classNameContains: [ 'Button' ] }, '@');
```

## [m#] classNameMatches

### classNameMatches(regex)

**`Global`** **`DEPRECATED`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression full match filter for the [class name selector](#m-classname).

- Filtering condition: The regular expression rule of the control's `className` fully matches the specified parameter.
- Associated control property: [className](uiObjectType#m-classname)

For example, for the following 4 controls:

```js
wA.className(); // android.view.View
wB.className(); // android.widget.Button
wC.className(); // android.widget.EditText
wD.className(); // androidx.recyclerview.widget.RecyclerView
```

`classNameMatches(/EditText/)` or `classNameMatches('EditText')` will not match any of the above controls (because `classNameMatches(/EditText/)` is equivalent to `classNameMatch(/^EditText$/)`).

`classNameMatches(/android.+View/)` or `classNameMatches('android.+View')` can match controls `wA` and `wD`, because `/^android.+View$/` matches their class names.

`classNameMatches(/Edit/)` or `classNameMatches('Edit')` will not match any of the above controls.

`classNameMatches(/.*Edit.*/)` or `classNameMatches('.*Edit.*')` can match control `wC`, because `/^.*Edit.*$/` matches its class name.

`classNameMatches(/V\w{0,3}/)` or `classNameMatches('V\\w{0,3}')` will not match any of the above controls.

`classNameMatches(/.*V\w{0,3}/)` or `classNameMatches('.*V\\w{0,3}')` can match controls `wA` and `wD`, because `/^.*V\w{0,3}$/` matches their class names.

[Pickup selector](#m-pickup) examples:

```js
pickup(classNameMatches(/.*V\w{0,3}/), '@');
pickup({ classNameMatches: /.*V\w{0,3}/ }, '@');
pickup({ classNameMatches: [ /.*V\w{0,3}/ ] }, '@');
```

> Note: Since version 6.2.0, classNameMatches has been deprecated. It is recommended to use [classNameMatch](#m-classnamematch). See the [Regular Expression Full Match Filter](#xxxmatches) section for details.

## [m#] classNameMatch

### classNameMatch(regex)

**`6.2.0`** **`Global`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression match filter for the [class name selector](#m-classname).

- Filtering condition: The regular expression rule of the control's `className` matches the specified parameter.
- Associated control property: [className](uiObjectType#m-classname)

For example, for the following 4 controls:

```js
wA.className(); // android.view.View
wB.className(); // android.widget.Button
wC.className(); // android.widget.EditText
wD.className(); // androidx.recyclerview.widget.RecyclerView
```

`classNameMatch(/EditText/)` or `classNameMatch('EditText')` can match control `wC`.  
`classNameMatch(/Edit/)` or `classNameMatch('Edit')` can also match control `wC`.

`classNameMatch(/^android/)` or `classNameMatch('^android')` can match controls `wA`, `wB`, `wC`, and `wD`.

`classNameMatch(/V\w{0,3}$/)` or `classNameMatch('V\\w{0,3}$')` can match controls `wA` and `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(classNameMatch(/V\w{0,3}$/), '@');
pickup({ classNameMatch: /V\w{0,3}$/ }, '@');
pickup({ classNameMatch: [ /V\w{0,3}$/ ] }, '@');
```

## [m#] packageName

### packageName(str)

**`Overload 1/2`** **`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Package name exact match selector.

- Filtering condition: The control's `packageName` exactly matches the specified string.
- Associated control property: [packageName](uiObjectType#m-packagename)

For example, for the following 4 controls:

```js
wA.packageName(); // org.mozilla.firefox
wB.packageName(); // com.microsoft.office.word
wC.packageName(); // com.twitter.android
wD.packageName(); // com.accuweather.android
```

`packageName('com.twitter.android')` is a package name selector that can match control `wC`.

`packageName('com.microsoft.office.word')` is also a package name selector that can match control `wB`.

[Pickup selector](#m-pickup) examples:

```js
pickup(packageName(com.microsoft.office.word), '@');
pickup({ packageName: com.microsoft.office.word }, '@');
pickup({ packageName: [ com.microsoft.office.word ] }, '@');
```

### packageName(app)

**`6.2.0`** **`Overload 2/2`** **`Global`**

- **app** { [App](appType) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Package name exact match selector.

- Filtering condition: The control's `packageName` exactly matches the package name of the specified [App enum class](appType) instance.
- Associated control property: [packageName](uiObjectType#m-packagename)

For example, for the following 4 controls:

```js
wA.packageName(); // org.mozilla.firefox
wB.packageName(); // com.microsoft.office.word
wC.packageName(); // com.twitter.android
wD.packageName(); // com.accuweather.android
```

`packageName(App.TWITTER)` is a package name selector that can match control `wC`; it uses an `App enum class` instance object as the filtering condition.

`packageName(App.WORD)` is also a package name selector that can match control `wB`.

[Pickup selector](#m-pickup) examples:

```js
pickup(packageName(App.WORD), '@');
pickup({ packageName: App.WORD }, '@');
pickup({ packageName: [ App.WORD ] }, '@');
```

## [m#] packageNameStartsWith

### packageNameStartsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Prefix match filter for the [package name selector](#m-packagename).

- Filtering condition: The control's `packageName` starts with the specified string.
- Associated control property: [packageName](uiObjectType#m-packagename)

For example, for the following 4 controls:

```js
wA.packageName(); // org.mozilla.firefox
wB.packageName(); // com.microsoft.office.word
wC.packageName(); // com.twitter.android
wD.packageName(); // com.accuweather.android
```

`packageNameStartsWith('com.')` is a package name prefix selector that can match controls `wB`, `wC`, and `wD`.

`packageNameStartsWith('com.a')` is also a package name prefix selector that can match control `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(packageNameStartsWith('com.a'), '@');
pickup({ packageNameStartsWith: 'com.a' }, '@');
pickup({ packageNameStartsWith: [ 'com.a' ] }, '@');
```

## [m#] packageNameEndsWith

### packageNameEndsWith(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Suffix match filter for the [package name selector](#m-packagename).

- Filtering condition: The control's `packageName` ends with the specified string.
- Associated control property: [packageName](uiObjectType#m-packagename)

For example, for the following 4 controls:

```js
wA.packageName(); // org.mozilla.firefox
wB.packageName(); // com.microsoft.office.word
wC.packageName(); // com.twitter.android
wD.packageName(); // com.accuweather.android
```

`packageNameEndsWith('android')` can match controls `wC` and `wD`.  
However, `packageNameEndsWith('Android')` cannot match any of the above controls, because package name matching is case-sensitive.

`packageNameEndsWith('firefox')` can match control `wA`.

[Pickup selector](#m-pickup) examples:

```js
pickup(packageNameEndsWith('firefox'), '@');
pickup({ packageNameEndsWith: 'firefox' }, '@');
pickup({ packageNameEndsWith: [ 'firefox' ] }, '@');
```

## [m#] packageNameContains

### packageNameContains(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Contains match filter for the [package name selector](#m-packagename).

- Filtering condition: The control's `packageName` matches the specified string for any length of consecutive characters.
- Associated control property: [packageName](uiObjectType#m-packagename)

For example, for the following 4 controls:

```js
wA.packageName(); // org.mozilla.firefox
wB.packageName(); // com.microsoft.office.word
wC.packageName(); // com.twitter.android
wD.packageName(); // com.accuweather.android
```

`packageNameContains('com')` can match controls `wB`, `wC`, and `wD`.

`packageNameContains('office')` can match control `wB`.

[Pickup selector](#m-pickup) examples:

```js
pickup(packageNameContains('office'), '@');
pickup({ packageNameContains: 'office' }, '@');
pickup({ packageNameContains: [ 'office' ] }, '@');
```

## [m#] packageNameMatches

### packageNameMatches(regex)

**`Global`** **`DEPRECATED`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression full match filter for the [package name selector](#m-packagename).

- Filtering condition: The regular expression rule of the control's `packageName` fully matches the specified parameter.
- Associated control property: [packageName](uiObjectType#m-packagename)

For example, for the following 4 controls:

```js
wA.packageName(); // org.mozilla.firefox
wB.packageName(); // com.microsoft.office.word
wC.packageName(); // com.twitter.android
wD.packageName(); // com.accuweather.android
```

`packageNameMatches(/office/)` or `packageNameMatches('office')` will not match any of the above controls (because `packageNameMatches(/office/)` is equivalent to `packageNameMatch(/^office$/)`).

`packageNameMatches(/com.+android/)` or `packageNameMatches('com.+android')` can match controls `wC` and `wD`, because `/^com.+android$/` matches their package names.

`packageNameMatches(/twitter/)` or `packageNameMatches('twitter')` will not match any of the above controls.

`packageNameMatches(/.*twitter.*/)` or `packageNameMatches('.*twitter.*')` can match control `wC`, because `/^.*twitter.*$/` matches its package name.

`packageNameMatches(/\.\w*r\w*d/)` or `packageNameMatches('\\.\\w*r\\w*d')` will not match any of the above controls.

`packageNameMatches(/.*\.\w*r\w*d/)` or `packageNameMatches('.*\\.\\w*r\\w*d')` can match controls `wB`, `wC`, and `wD`, because `/^.*\.\w*r\w*d$/` matches their package names.

[Pickup selector](#m-pickup) examples:

```js
pickup(packageNameMatches(/.*\.\w*r\w*d/), '@');
pickup({ packageNameMatches: /.*\.\w*r\w*d/ }, '@');
pickup({ packageNameMatches: [ /.*\.\w*r\w*d/ ] }, '@');
```

> Note: Since version 6.2.0, packageNameMatches has been deprecated. It is recommended to use [packageNameMatch](#m-packagenamematch). See the [Regular Expression Full Match Filter](#xxxmatches) section for details.

## [m#] packageNameMatch

### packageNameMatch(regex)

**`6.2.0`** **`Global`**

- **regex** { [string](dataTypes#string) | [RegExp](dataTypes#regexp) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Regular expression match filter for the [package name selector](#m-packagename).

- Filtering condition: The regular expression rule of the control's `packageName` matches the specified parameter.
- Associated control property: [packageName](uiObjectType#m-packagename)

For example, for the following 4 controls:

```js
wA.packageName(); // org.mozilla.firefox
wB.packageName(); // com.microsoft.office.word
wC.packageName(); // com.twitter.android
wD.packageName(); // com.accuweather.android
```

`packageNameMatch(/office/)` or `packageNameMatch('office')` can match control `wC`.

`packageNameMatch(/android$/)` or `packageNameMatch('android$')` can match controls `wC` and `wD`.

`packageNameMatch(/\.\w*r\w*d$/)` or `packageNameMatch('\\.\\w*r\\w*d$')` can match controls `wB`, `wC`, and `wD`.

[Pickup selector](#m-pickup) examples:

```js
pickup(packageNameMatch(/\.\w*r\w*d$/), '@');
pickup({ packageNameMatch: /\.\w*r\w*d$/ }, '@');
pickup({ packageNameMatch: [ /\.\w*r\w*d$/ ] }, '@');
```

## [m#] currentApp

### currentApp(app)

**`6.2.0`** **`Overload 1/2`** **`Global`**

- **app** { [App](appType) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Application selector.

- Filtering condition: The control's `packageName` exactly matches the package name of the specified [App enum class](appType) instance.
- Associated control property: [packageName](uiObjectType#m-packagename)

When `currentApp` receives an `App enum class` instance, it has the same effect as [packageName(app)](#packagenameapp).

For example, for the following 4 controls:

```js
wA.packageName(); // org.mozilla.firefox
wB.packageName(); // com.microsoft.office.word
wC.packageName(); // com.twitter.android
wD.packageName(); // com.accuweather.android
```

`currentApp(App.TWITTER)` is an application selector that can match control `wC`.  
`packageName(App.TWITTER)` is a [package name selector](#m-packagename) with the same effect as the above selector.

`currentApp(App.WORD)` is also an application selector that can match control `wB`.
`packageName(App.WORD)` has the same effect as the above selector.

[Pickup selector](#m-pickup) examples:

```js
pickup(currentApp(App.WORD), '@');
pickup({ currentApp: App.WORD }, '@');
pickup({ currentApp: [ App.WORD ] }, '@');
```

### currentApp(name)

**`6.2.0`** **`Overload 2/2`** **`Global`**

- **name** { [string](dataTypes#string) } - [Alias / Current language app name / Simplified Chinese app name / English app name] of the App enum class instance.
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Application selector.

- Filtering condition: The control's `packageName` exactly matches the package name of the [App enum class](appType) instance corresponding to the specified parameter.
- Associated control property: [packageName](uiObjectType#m-packagename)

1. Parse the `name` parameter and determine the unique `App enum class` instance using [alias / current language app name / Simplified Chinese app name / English app name].
2. Obtain the package name of the above `App enum class` instance as the reference value.
3. Filter controls whose package name matches the above reference value.

For example, for the following control:

```js
w.packageName(); // com.eg.android.AlipayGphone
```

`currentApp('支付宝')` is an application selector that can match control `w`; it uses the Simplified Chinese app name of the `App enum class` instance as the filtering condition. (Example kept for accuracy)

`currentApp('Alipay')` is an application selector that can match control `w`; it uses the English app name of the `App enum class` instance as the filtering condition.

`currentApp('alipay')` is an application selector that can match control `w`; it uses the alias of the `App enum class` instance as the filtering condition.

[Pickup selector](#m-pickup) examples:

```js
pickup(currentApp('alipay'), '@');
pickup({ currentApp: 'alipay' }, '@');
pickup({ currentApp: [ 'alipay' ] }, '@');
```

## [m#] bounds

### bounds(left, top, right, bottom)

**`[6.2.0]`** **`Global`**

- **left** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle left boundary X coordinate or percentage
- **top** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle top boundary Y coordinate or percentage
- **right** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle right boundary X coordinate or percentage
- **bottom** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle bottom boundary Y coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) selector.

- Filtering condition: The control's rectangle exactly matches the specified boundary parameters.
- Associated control property: [bounds](uiObjectType#m-bounds)

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(0, 48 - 112, 160)
wB.bounds(); // Rect(0, 192 - 972, 1728)
wC.bounds(); // Rect(0, 192 - 1080, 1920)
```

`bounds(0, 48, 112, 160)` is a control rectangle selector that can match control `wA`; it uses 4 absolute coordinate values as filtering conditions.

`bounds(0, 0.1, 0.9, 0.9)` is a control rectangle selector that may match control `wB`; it uses percentages of screen width and height as filtering conditions.

`bounds(0, 192, -1, -1)` is a control rectangle selector that may match control `wC`; it uses absolute coordinate values and screen dimension reference values as filtering conditions.

When printing selector information, percentage parameters are shown as approximate values with three decimal places:

```js
/* Device screen: 1080 × 1920. */

console.log(655 / device.width); // 0.6064814814814815
console.log(bounds(655 / device.width, 0.1, 0.9, 0.9)); // bounds(0.606, 0.1, 0.9, 0.9)
```

When converting percentage parameters to actual pixel values for filtering, if the value is an integer, it is used directly; if not, the two nearest integers are filtered simultaneously:

```js
/* Device screen: 1080 × 1920. */

/* For selector bounds(0.606, 0.1, 0.9, 0.9). */

console.log('left: ' + 0.606 * device.width); // 654.48
console.log('top: ' + 0.1 * device.height); // 192
console.log('right: ' + 0.9 * device.width); // 972
console.log('bottom: ' + 0.9 * device.height); // 1728

/* Note that the left coordinate is not an integer, so both left coordinates 654 and 655 will be filtered. */
/* If a control w has bounds Rect(655, 192 - 972, 1728), it will be matched by the above selector. */
```

[Pickup selector](#m-pickup) examples:

```js
pickup(bounds(0, 192, -1, -1), '@');
pickup({ bounds: [ 0, 192, -1, -1 ] }, '@');
```

## [m#] boundsInside

### boundsInside(left, top, right, bottom)

**`[6.2.0]`** **`Global`**

- **left** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle left boundary X coordinate or percentage
- **top** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle top boundary Y coordinate or percentage
- **right** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle right boundary X coordinate or percentage
- **bottom** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle bottom boundary Y coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) selector.

- Filtering condition: The control's rectangle is completely inside the specified boundaries.
- Associated control property: [bounds](uiObjectType#m-bounds)

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(0, 48 - 112, 160)
wB.bounds(); // Rect(0, 192 - 972, 1728)
wC.bounds(); // Rect(0, 192 - 1080, 1920)
```

`boundsInside(0, 32, 112, 160)` is a control rectangle selector that can match control `wA`; it uses 4 absolute coordinate values as filtering conditions.

`boundsInside(0, 0.02, 0.95, 0.95)` is a control rectangle selector that may match control `wB`; it uses percentages of screen width and height as filtering conditions.

`boundsInside(0, 128, -1, -1)` is a control rectangle selector that may match controls `wB` and `wC`; it uses absolute coordinate values and screen dimension reference values as filtering conditions.

`boundsInside(0, 0, -1, -1)` is a special control rectangle filter that selects controls whose entire bounds are inside the screen. Therefore `wA`, `wB`, and `wC` can all be matched, but `Rect(0, -10 - 20, 20)` cannot because its `top` coordinate is out of bounds.

When printing selector information, percentage parameters are shown as approximate values with three decimal places:

```js
/* Device screen: 1080 × 1920. */

console.log(655 / device.width); // 0.6064814814814815
console.log(boundsInside(655 / device.width, 0.1, 0.9, 0.9)); // boundsInside(0.606, 0.1, 0.9, 0.9)
```

When converting percentage parameters to actual pixel values for filtering, if the value is an integer, it is used directly; if not, the boundaries undergo [control rectangle expansion](glossaries#control-rectangle-expansion):

```js
/* Device screen: 1080 × 1920. */

/* For selector boundsInside(0.606, 0.1, 0.9, 0.9). */

console.log('left: ' + 0.606 * device.width); // 654.48
console.log('top: ' + 0.1 * device.height); // 192
console.log('right: ' + 0.9 * device.width); // 972
console.log('bottom: ' + 0.9 * device.height); // 1728

/* Note that the left coordinate is not an integer, so left will be expanded to 654. */
/* If a control w has bounds Rect(655, 192 - 972, 1728), it will be matched by the above selector. */
```

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsInside(0, 0.02, 0.95, 0.95), '@');
pickup({ boundsInside: [ 0, 0.02, 0.95, 0.95 ] }, '@');
```

## [m#] boundsContains

### boundsContains(left, top, right, bottom)

**`[6.2.0]`** **`Global`**

- **left** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle left boundary X coordinate or percentage
- **top** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle top boundary Y coordinate or percentage
- **right** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle right boundary X coordinate or percentage
- **bottom** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle bottom boundary Y coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) selector.

- Filtering condition: The control's rectangle completely contains the specified boundaries.
- Associated control property: [bounds](uiObjectType#m-bounds)

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(0, 48 - 112, 160)
wB.bounds(); // Rect(0, 192 - 972, 1728)
wC.bounds(); // Rect(0, 192 - 1080, 1920)
```

`boundsContains(0, 55, 112, 160)` is a control rectangle selector that can match control `wA`; it uses 4 absolute coordinate values as filtering conditions.

`boundsContains(0, 0.3, 0.85, 0.85)` is a control rectangle selector that may match controls `wB` and `wC`; it uses percentages of screen width and height as filtering conditions.

`boundsContains(0, 0.3, -1, -1)` is a control rectangle selector that may match control `wC`; it uses absolute coordinate values and screen dimension reference values as filtering conditions.

When printing selector information, percentage parameters are shown as approximate values with three decimal places:

```js
/* Device screen: 1080 × 1920. */

console.log(655 / device.width); // 0.6064814814814815
console.log(boundsContains(655 / device.width, 0.1, 0.9, 0.9)); // boundsContains(0.606, 0.1, 0.9, 0.9)
```

When converting percentage parameters to actual pixel values for filtering, if the value is an integer, it is used directly; if not, the boundaries undergo [control rectangle contraction](glossaries#control-rectangle-contraction):

```js
/* Device screen: 1080 × 1920. */

/* For selector boundsContains(0.606, 0.1, 0.9, 0.9). */

console.log('left: ' + 0.606 * device.width); // 654.48
console.log('top: ' + 0.1 * device.height); // 192
console.log('right: ' + 0.9 * device.width); // 972
console.log('bottom: ' + 0.9 * device.height); // 1728

/* Note that the left coordinate is not an integer, so left will be contracted to 655. */
/* If a control w has bounds Rect(655, 192 - 972, 1728), it will be matched by the above selector. */
```

In addition to "rectangular region" constraints, the boundsContains selector can also be used for "line region" or even "point region" constraints:

```js
/* "Line region" constraint. */
boundsContains(0.23, 0.1, 0.23, 0.98); /* Note that left and right are the same. */
boundsContains(0.1, 0.75, 0.9, 0.75); /* Note that top and bottom are the same. */

/* "Point region" constraint. */
boundsContains(0.23, 0.1, 0.23, 0.1); /* Note that left and right are the same, and top and bottom are the same. */
```

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsContains(0, 0.3, 0.85, 0.85), '@');
pickup({ boundsContains: [ 0, 0.3, 0.85, 0.85 ] }, '@');
```

## [m#] boundsLeft

### boundsLeft(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle left boundary X coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The left boundary of the control's rectangle matches the specified value.
- Associated control property: [ [boundsLeft](uiObjectType#m-boundsleft) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(108, 48 - 112, 160)
wB.bounds(); // Rect(108, 96 - 256, 1280)
wC.bounds(); // Rect(108, 112 - 1040, 1600)
```

`boundsLeft(108)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses an absolute coordinate value as the filtering condition.

`boundsLeft(0.1)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsLeft(0.1), '@');
pickup({ boundsLeft: 0.1 }, '@');
```

### boundsLeft(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for the rectangle's left boundary (as X coordinate or percentage)
- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for the rectangle's left boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The left boundary of the control's rectangle matches the specified boundary range.
- Associated control property: [ [boundsLeft](uiObjectType#m-boundsleft) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(108, 48 - 112, 160)
wB.bounds(); // Rect(108, 96 - 256, 1280)
wC.bounds(); // Rect(108, 112 - 1040, 1600)
```

`boundsLeft(100, 200)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses absolute coordinate values as the filtering condition.

`boundsLeft(0.05, 0.15)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses screen width percentages as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsLeft(0.05, 0.15), '@');
pickup({ boundsLeft: [ 0.05, 0.15 ] }, '@');
```

## [m#] boundsTop

### boundsTop(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle top boundary Y coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The top boundary of the control's rectangle matches the specified value.
- Associated control property: [ [boundsTop](uiObjectType#m-boundstop) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 96 - 112, 160)
wB.bounds(); // Rect(30, 96 - 256, 1280)
wC.bounds(); // Rect(24, 96 - 1040, 1600)
```

`boundsTop(96)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses an absolute coordinate value as the filtering condition.

`boundsTop(0.05)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen height percentage as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsTop(0.1), '@');
pickup({ boundsTop: 0.1 }, '@');
```

### boundsTop(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for the rectangle's top boundary (as Y coordinate or percentage)
- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for the rectangle's top boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The top boundary of the control's rectangle matches the specified boundary range.
- Associated control property: [ [boundsTop](uiObjectType#m-boundstop) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 96 - 112, 160)
wB.bounds(); // Rect(30, 96 - 256, 1280)
wC.bounds(); // Rect(24, 96 - 1040, 1600)
```

`boundsTop(60, 120)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses absolute coordinate values as the filtering condition.

`boundsTop(0.02, 0.12)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses screen height percentages as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsTop(0.02, 0.12), '@');
pickup({ boundsTop: [ 0.02, 0.12 ] }, '@');
```

## [m#] boundsRight

### boundsRight(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle right boundary X coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The right boundary of the control's rectangle matches the specified value.
- Associated control property: [ [boundsRight](uiObjectType#m-boundsright) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wB.bounds(); // Rect(50, 96 - 256, 1280)
wC.bounds(); // Rect(66, 112 - 256, 1600)
```

`boundsRight(256)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses absolute coordinate values as the filtering condition.

`boundsRight(0.237)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses screen width percentages as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsRight(0.237), '@');
pickup({ boundsRight: 0.237 }, '@');
```

### boundsRight(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for the rectangle's right boundary (as X coordinate or percentage)
- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for the rectangle's right boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The right boundary of the control's rectangle matches the specified boundary range
- Associated control property: [ [boundsRight](uiObjectType#m-boundsright) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wB.bounds(); // Rect(50, 96 - 256, 1280)
wC.bounds(); // Rect(66, 112 - 256, 1600)
```

`boundsRight(210, 320)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses absolute coordinate values as the filtering condition.

`boundsRight(0.2, 0.25)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses screen width percentages as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsRight(0.2, 0.25), '@');
pickup({ boundsRight: [ 0.2, 0.25 ] }, '@');
```

## [m#] boundsBottom

### boundsBottom(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle bottom boundary Y coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The bottom boundary of the control's rectangle matches the specified value
- Associated control property: [ [boundsBottom](uiObjectType#m-boundsbottom) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wB.bounds(); // Rect(30, 96 - 256, 1632)
wC.bounds(); // Rect(24, 112 - 1040, 1632)
```

`boundsBottom(1632)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses absolute coordinate values as the filtering condition.

`boundsBottom(0.85)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses screen height percentages as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsBottom(0.85), '@');
pickup({ boundsBottom: 0.85 }, '@');
```

### boundsBottom(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for the rectangle's bottom boundary (as Y coordinate or percentage)
- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for the rectangle's bottom boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The bottom boundary of the control's rectangle matches the specified boundary range.
- Associated control property: [ [boundsBottom](uiObjectType#m-boundsbottom) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wB.bounds(); // Rect(30, 96 - 256, 1632)
wC.bounds(); // Rect(24, 112 - 1040, 1632)
```

`boundsBottom(1600, -1)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses absolute coordinate values and screen height reference values as the filtering condition.

`boundsBottom(0.8, 0.9)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses screen height percentages as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsBottom(0.8, 0.9), '@');
pickup({ boundsBottom: [ 0.8, 0.9 ] }, '@');
```

## [m#] boundsWidth

### boundsWidth(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle width (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The width of the control's rectangle matches the specified measurement.
- Associated control property: [ [boundsWidth](uiObjectType#m-boundswidth) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wA.boundsWidth(); // 238
wB.bounds(); // Rect(50, 96 - 256, 1280)
wB.boundsWidth(); // 206
wC.bounds(); // Rect(66, 112 - 256, 1600)
wC.boundsWidth(); // 190
```

`boundsWidth(206)` is a control rectangle size selector that can match control `wB`; it uses a width value as the filtering condition.

`boundsWidth(0.191)` is also a control rectangle size selector that may match control `wB`; it uses a screen width percentage as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsWidth(206), '@');
pickup({ boundsWidth: 206 }, '@');
```

### boundsWidth(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum rectangle width (as absolute value or percentage)
- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum rectangle width (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The width of the control's rectangle matches the specified measurement range.
- Associated control property: [ [boundsWidth](uiObjectType#m-boundswidth) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wA.boundsWidth(); // 238
wB.bounds(); // Rect(50, 96 - 256, 1280)
wB.boundsWidth(); // 206
wC.bounds(); // Rect(66, 112 - 256, 1600)
wC.boundsWidth(); // 190
```

`boundsWidth(150, 300)` is a control rectangle size selector that can match controls `wA`, `wB`, and `wC`; it uses width values as the filtering condition.

`boundsWidth(0.139, 0.278)` is also a control rectangle size selector that may match controls `wA`, `wB`, and `wC`; it uses screen width percentages as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsWidth(0.139, 0.278), '@');
pickup({ boundsWidth: [ 0.139, 0.278 ] }, '@');
```

## [m#] boundsHeight

### boundsHeight(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle height (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The height of the control's rectangle matches the specified measurement.
- Associated control property: [ [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wA.boundsHeight(); // 1584
wB.bounds(); // Rect(30, 96 - 256, 1632)
wB.boundsHeight(); // 1536
wC.bounds(); // Rect(24, 112 - 1040, 1632)
wC.boundsHeight(); // 1520
```

`boundsHeight(1536)` is a control rectangle size selector that can match control `wB`; it uses a height value as the filtering condition.

`boundsHeight(0.8)` is also a control rectangle size selector that may match control `wB`; it uses a screen height percentage as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsHeight(0.8), '@');
pickup({ boundsHeight: 0.8 }, '@');
```

### boundsHeight(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum rectangle height (as absolute value or percentage)
- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum rectangle height (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The height of the control's rectangle matches the specified measurement range.
- Associated control property: [ [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wA.boundsHeight(); // 1584
wB.bounds(); // Rect(30, 96 - 256, 1632)
wB.boundsHeight(); // 1536
wC.bounds(); // Rect(24, 112 - 1040, 1632)
wC.boundsHeight(); // 1520
```

`boundsHeight(1500, -1)` is a control rectangle size selector that can match controls `wA`, `wB`, and `wC`; it uses height values and screen height reference values as the filtering condition.

`boundsHeight(0.781, 0.982)` is also a control rectangle size selector that may match controls `wA`, `wB`, and `wC`; it uses screen height percentages as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsHeight(0.781, 0.982), '@');
pickup({ boundsHeight: [ 0.781, 0.982 ] }, '@');
```

## [m#] boundsCenterX

### boundsCenterX(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle center point X coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The X coordinate of the center point of the control's rectangle matches the specified value.
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wA.boundsCenterX(); // 137
wB.bounds(); // Rect(50, 96 - 256, 1280)
wB.boundsCenterX(); // 153
wC.bounds(); // Rect(66, 112 - 256, 1600)
wC.boundsCenterX(); // 161
```

`boundsCenterX(153)` is a control rectangle center point selector that can match control `wB`; it uses a coordinate value as the filtering condition.

`boundsCenterX(0.142)` is also a control rectangle center point selector that may match control `wB`; it uses a screen width percentage as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsCenterX(0.142), '@');
pickup({ boundsCenterX: 0.142 }, '@');
```

### boundsCenterX(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum center point X coordinate (as value or percentage)
- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum center point X coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The X coordinate of the center point of the control's rectangle matches the specified range.
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wA.boundsCenterX(); // 137
wB.bounds(); // Rect(50, 96 - 256, 1280)
wB.boundsCenterX(); // 153
wC.bounds(); // Rect(66, 112 - 256, 1600)
wC.boundsCenterX(); // 161
```

`boundsCenterX(120, 240)` is a control rectangle center point selector that can match controls `wA`, `wB`, and `wC`; it uses coordinate values as the filtering condition.

`boundsCenterX(0.111, 0.222)` is also a control rectangle center point selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsCenterX(0.111, 0.222), '@');
pickup({ boundsCenterX: [ 0.111, 0.222 ] }, '@');
```

## [m#] boundsCenterY

### boundsCenterY(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle center point Y coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The Y coordinate of the center point of the control's rectangle matches the specified value.
- Associated control property: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wA.boundsCenterY(); // 840
wB.bounds(); // Rect(30, 96 - 256, 1632)
wB.boundsCenterY(); // 864
wC.bounds(); // Rect(24, 112 - 1040, 1632)
wC.boundsCenterY(); // 872
```

`boundsCenterY(864)` is a control rectangle center point selector that can match control `wB`; it uses a coordinate value as the filtering condition.

`boundsCenterY(0.45)` is also a control rectangle center point selector that may match control `wB`; it uses a screen height percentage as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsCenterY(0.45), '@');
pickup({ boundsCenterY: 0.45 }, '@');
```

### boundsCenterY(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum center point Y coordinate (as value or percentage)
- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum center point Y coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The Y coordinate of the center point of the control's rectangle matches the specified range.
- Associated control property: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wA.boundsCenterY(); // 840
wB.bounds(); // Rect(30, 96 - 256, 1632)
wB.boundsCenterY(); // 864
wC.bounds(); // Rect(24, 112 - 1040, 1632)
wC.boundsCenterY(); // 872
```

`boundsCenterY(800, 900)` is a control rectangle center point selector that can match controls `wA`, `wB`, and `wC`; it uses coordinate values as the filtering condition.

`boundsCenterY(0.417, 0.469)` is also a control rectangle center point selector that may match controls `wA`, `wB`, and `wC`; it uses screen height percentages as the filtering condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsCenterY(0.417, 0.469), '@');
pickup({ boundsCenterY: [ 0.417, 0.469 ] }, '@');
```

## [m#] boundsMinLeft

### boundsMinLeft(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for the rectangle's left boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The left boundary of the control's rectangle matches the specified minimum boundary.
- Associated control property: [ [boundsLeft](uiObjectType#m-boundsleft) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(108, 48 - 112, 160)
wB.bounds(); // Rect(108, 96 - 256, 1280)
wC.bounds(); // Rect(108, 112 - 1040, 1600)
```

`boundsMinLeft(100)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses absolute coordinate values as the filtering condition.

`boundsMinLeft(0.05)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMinLeft(0.05), '@');
pickup({ boundsMinLeft: 0.05 }, '@');
```

## [m#] boundsMinTop

### boundsMinTop(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for the rectangle's top boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The top boundary of the control's rectangle matches the specified boundary limit
- Associated control property: [ [boundsTop](uiObjectType#m-boundstop) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 96 - 112, 160)
wB.bounds(); // Rect(30, 96 - 256, 1280)
wC.bounds(); // Rect(24, 96 - 1040, 1600)
```

`boundsMinTop(60)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses absolute coordinate values as the filtering condition.

`boundsMinTop(0.02)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen height percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMinTop(0.02), '@');
pickup({ boundsMinTop: 0.02 }, '@');
```

## [m#] boundsMinRight

### boundsMinRight(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for the rectangle's right boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The right boundary of the control's rectangle matches the specified boundary range
- Associated control property: [ [boundsRight](uiObjectType#m-boundsright) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wB.bounds(); // Rect(50, 96 - 256, 1280)
wC.bounds(); // Rect(66, 112 - 256, 1600)
```

`boundsMinRight(210)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses an absolute coordinate value as the filter condition.

`boundsMinRight(0.2)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMinRight(0.2), '@');
pickup({ boundsMinRight: 0.2 }, '@');
```

## [m#] boundsMinBottom

### boundsMinBottom(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for the rectangle's bottom boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The bottom boundary of the control's rectangle matches the specified boundary range.
- Associated control property: [ [boundsBottom](uiObjectType#m-boundsbottom) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wB.bounds(); // Rect(30, 96 - 256, 1632)
wC.bounds(); // Rect(24, 112 - 1040, 1632)
```

`boundsMinBottom(1600)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses an absolute coordinate value as the filter condition.

`boundsMinBottom(0.8)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen height percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMinBottom(0.8), '@');
pickup({ boundsMinBottom: 0.8 }, '@');
```

## [m#] boundsMinWidth

### boundsMinWidth(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for rectangle width (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The width of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsWidth](uiObjectType#m-boundswidth) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wA.boundsMinWidth(); // 238
wB.bounds(); // Rect(50, 96 - 256, 1280)
wB.boundsMinWidth(); // 206
wC.bounds(); // Rect(66, 112 - 256, 1600)
wC.boundsMinWidth(); // 190
```

`boundsMinWidth(150)` is a control rectangle size selector that can match controls `wA`, `wB`, and `wC`; it uses width values as the filtering condition.

`boundsMinWidth(0.139)` is also a control rectangle size selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMinWidth(0.139), '@');
pickup({ boundsMinWidth: 0.139 }, '@');
```

## [m#] boundsMinHeight

### boundsMinHeight(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for rectangle height (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The height of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wA.boundsMinHeight(); // 1584
wB.bounds(); // Rect(30, 96 - 256, 1632)
wB.boundsMinHeight(); // 1536
wC.bounds(); // Rect(24, 112 - 1040, 1632)
wC.boundsMinHeight(); // 1520
```

`boundsMinHeight(1500)` is a control rectangle size selector that can match controls `wA`, `wB`, and `wC`; it uses a height value as the filter condition.

`boundsMinHeight(0.781)` is also a control rectangle size selector that may match controls `wA`, `wB`, and `wC`; it uses a screen height percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMinHeight(0.781), '@');
pickup({ boundsMinHeight: 0.781 }, '@');
```

## [m#] boundsMinCenterX

### boundsMinCenterX(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum center point X coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The X coordinate of the center point of the control's rectangle matches the specified range.
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wA.boundsMinCenterX(); // 137
wB.bounds(); // Rect(50, 96 - 256, 1280)
wB.boundsMinCenterX(); // 153
wC.bounds(); // Rect(66, 112 - 256, 1600)
wC.boundsMinCenterX(); // 161
```

`boundsMinCenterX(120)` is a control rectangle center point selector that can match controls `wA`, `wB`, and `wC`; it uses a coordinate value as the filter condition.

`boundsMinCenterX(0.111)` is also a control rectangle center point selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMinCenterX(0.111), '@');
pickup({ boundsMinCenterX: 0.111 }, '@');
```

## [m#] boundsMinCenterY

### boundsMinCenterY(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum center point Y coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The Y coordinate of the center point of the control's rectangle matches the specified coordinate limit.
- Associated control properties: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wA.boundsMinCenterY(); // 840
wB.bounds(); // Rect(30, 96 - 256, 1632)
wB.boundsMinCenterY(); // 864
wC.bounds(); // Rect(24, 112 - 1040, 1632)
wC.boundsMinCenterY(); // 872
```

`boundsMinCenterY(800)` is a control rectangle center point selector that can match controls `wA`, `wB`, and `wC`; it uses a coordinate value as the filter condition.

`boundsMinCenterY(0.417)` is also a control rectangle center point selector that may match controls `wA`, `wB`, and `wC`; it uses a screen height percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMinCenterY(0.417), '@');
pickup({ boundsMinCenterY: 0.417 }, '@');
```

## [m#] boundsMaxLeft

### boundsMaxLeft(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for the rectangle's left boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The left boundary of the control's rectangle matches the specified boundary limit.
- Associated control property: [ [boundsLeft](uiObjectType#m-boundsleft) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(108, 48 - 112, 160)
wB.bounds(); // Rect(108, 96 - 256, 1280)
wC.bounds(); // Rect(108, 112 - 1040, 1600)
```

`boundsMaxLeft(200)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses an absolute coordinate value as the filter condition.

`boundsMaxLeft(0.15)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMaxLeft(0.15), '@');
pickup({ boundsMaxLeft: 0.15 }, '@');
```

## [m#] boundsMaxTop

### boundsMaxTop(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for the rectangle's top boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The top boundary of the control's rectangle matches the specified boundary limit
- Associated control property: [ [boundsTop](uiObjectType#m-boundstop) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 96 - 112, 160)
wB.bounds(); // Rect(30, 96 - 256, 1280)
wC.bounds(); // Rect(24, 96 - 1040, 1600)
```

`boundsMaxTop(120)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses an absolute coordinate value as the filter condition.

`boundsMaxTop(0.12)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen height percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMaxTop(0.12), '@');
pickup({ boundsMaxTop: 0.12 }, '@');
```

## [m#] boundsMaxRight

### boundsMaxRight(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for the rectangle's right boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The right boundary of the control's rectangle matches the specified boundary range
- Associated control property: [ [boundsRight](uiObjectType#m-boundsright) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wB.bounds(); // Rect(50, 96 - 256, 1280)
wC.bounds(); // Rect(66, 112 - 256, 1600)
```

`boundsMaxRight(320)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses an absolute coordinate value as the filter condition.

`boundsMaxRight(0.25)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMaxRight(0.25), '@');
pickup({ boundsMaxRight: 0.25 }, '@');
```

## [m#] boundsMaxBottom

### boundsMaxBottom(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for the rectangle's bottom boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The bottom boundary of the control's rectangle matches the specified boundary range.
- Associated control property: [ [boundsBottom](uiObjectType#m-boundsbottom) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wB.bounds(); // Rect(30, 96 - 256, 1632)
wC.bounds(); // Rect(24, 112 - 1040, 1632)
```

`boundsMaxBottom(-1)` is a control rectangle boundary selector that can match controls `wA`, `wB`, and `wC`; it uses a screen height special value as the filter condition.

`boundsMaxBottom(0.9)` is also a control rectangle boundary selector that may match controls `wA`, `wB`, and `wC`; it uses a screen height percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMaxBottom(0.9), '@');
pickup({ boundsMaxBottom: 0.9 }, '@');
```

## [m#] boundsMaxWidth

### boundsMaxWidth(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for rectangle width (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The width of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsWidth](uiObjectType#m-boundswidth) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wA.boundsMaxWidth(); // 238
wB.bounds(); // Rect(50, 96 - 256, 1280)
wB.boundsMaxWidth(); // 206
wC.bounds(); // Rect(66, 112 - 256, 1600)
wC.boundsMaxWidth(); // 190
```

`boundsMaxWidth(300)` is a control rectangle size selector that can match controls `wA`, `wB`, and `wC`; it uses width values as the filtering condition.

`boundsMaxWidth(0.278)` is also a control rectangle size selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMaxWidth(0.278), '@');
pickup({ boundsMaxWidth: 0.278 }, '@');
```

## [m#] boundsMaxHeight

### boundsMaxHeight(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for rectangle height (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The height of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wA.boundsMaxHeight(); // 1584
wB.bounds(); // Rect(30, 96 - 256, 1632)
wB.boundsMaxHeight(); // 1536
wC.bounds(); // Rect(24, 112 - 1040, 1632)
wC.boundsMaxHeight(); // 1520
```

`boundsMaxHeight(-1)` is a control rectangle size selector that can match controls `wA`, `wB`, and `wC`; it uses a screen height special value as the filter condition.

`boundsMaxHeight(0.982)` is also a control rectangle size selector that may match controls `wA`, `wB`, and `wC`; it uses a screen height percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMaxHeight(0.982), '@');
pickup({ boundsMaxHeight: 0.982 }, '@');
```

## [m#] boundsMaxCenterX

### boundsMaxCenterX(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum center point X coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The X coordinate of the center point of the control's rectangle matches the specified range.
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(18, 48 - 256, 160)
wA.boundsMaxCenterX(); // 137
wB.bounds(); // Rect(50, 96 - 256, 1280)
wB.boundsMaxCenterX(); // 153
wC.bounds(); // Rect(66, 112 - 256, 1600)
wC.boundsMaxCenterX(); // 161
```

`boundsMaxCenterX(240)` is a control rectangle center point selector that can match controls `wA`, `wB`, and `wC`; it uses a coordinate value as the filter condition.

`boundsMaxCenterX(0.222)` is also a control rectangle center point selector that may match controls `wA`, `wB`, and `wC`; it uses a screen width percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMaxCenterX(0.222), '@');
pickup({ boundsMaxCenterX: 0.222 }, '@');
```

## [m#] boundsMaxCenterY

### boundsMaxCenterY(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum center point Y coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The Y coordinate of the center point of the control's rectangle matches the specified coordinate limit.
- Associated control properties: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
wA.bounds(); // Rect(10, 48 - 112, 1632)
wA.boundsMaxCenterY(); // 840
wB.bounds(); // Rect(30, 96 - 256, 1632)
wB.boundsMaxCenterY(); // 864
wC.bounds(); // Rect(24, 112 - 1040, 1632)
wC.boundsMaxCenterY(); // 872
```

`boundsMaxCenterY(900)` is a control rectangle center point selector that can match controls `wA`, `wB`, and `wC`; it uses a coordinate value as the filter condition.

`boundsMaxCenterY(0.469)` is also a control rectangle center point selector that may match controls `wA`, `wB`, and `wC`; it uses a screen height percentage as the filter condition.

When converting percentage parameters to pixel coordinates for filtering, if the value is an integer, it is used directly; if not, the value is rounded.

[Pickup selector](#m-pickup) examples:

```js
pickup(boundsMaxCenterY(0.469), '@');
pickup({ boundsMaxCenterY: 0.469 }, '@');
```

## [m#] left

### left(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle left boundary X coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The left boundary of the control's rectangle matches the specified boundary.
- Associated control property: [ [boundsLeft](uiObjectType#m-boundsleft) / [bounds](uiObjectType#m-bounds) ]

Alias of [UiSelector#boundsLeft](#boundsleftvalue).

### left(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for the rectangle's left boundary (as X coordinate or percentage)
- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for the rectangle's left boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The left boundary of the control's rectangle matches the specified boundary limit.
- Associated control property: [ [boundsLeft](uiObjectType#m-boundsleft) / [bounds](uiObjectType#m-bounds) ]

Alias of [UiSelector#boundsLeft](#boundsleftmin-max).

## [m#] top

### top(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle top boundary Y coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The top boundary of the control's rectangle matches the specified boundary.
- Associated control property: [ [boundsTop](uiObjectType#m-boundstop) / [bounds](uiObjectType#m-bounds) ]

Alias of [UiSelector#boundsTop](#boundstopvalue).

### top(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for the rectangle's top boundary (as Y coordinate or percentage)
- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for the rectangle's top boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The top boundary of the control's rectangle matches the specified boundary limit
- Associated control property: [ [boundsTop](uiObjectType#m-boundstop) / [bounds](uiObjectType#m-bounds) ]

Alias of [UiSelector#boundsTop](#boundstopmin-max).

## [m#] right

### right(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle right boundary X coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The right boundary of the control's rectangle matches the specified boundary.
- Associated control property: [ [boundsRight](uiObjectType#m-boundsright) / [bounds](uiObjectType#m-bounds) ]

Alias of [UiSelector#boundsRight](#boundsrightvalue).

### right(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for the rectangle's right boundary (as X coordinate or percentage)
- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for the rectangle's right boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The right boundary of the control's rectangle matches the specified boundary range
- Associated control property: [ [boundsRight](uiObjectType#m-boundsright) / [bounds](uiObjectType#m-bounds) ]

Alias of [UiSelector#boundsRight](#boundsrightmin-max).

## [m#] bottom

### bottom(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle bottom boundary Y coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The bottom boundary of the control's rectangle matches the specified value
- Associated control property: [ [boundsBottom](uiObjectType#m-boundsbottom) / [bounds](uiObjectType#m-bounds) ]

Alias of [UiSelector#boundsBottom](#boundsbottomvalue).

### bottom(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for the rectangle's bottom boundary (as Y coordinate or percentage)
- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for the rectangle's bottom boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The bottom boundary of the control's rectangle matches the specified boundary range.
- Associated control property: [ [boundsBottom](uiObjectType#m-boundsbottom) / [bounds](uiObjectType#m-bounds) ]

Alias of [UiSelector#boundsBottom](#boundsbottommin-max).

## [m#] width

### width(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle width (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The width of the control's rectangle matches the specified measurement
- Associated control property: [ [boundsWidth](uiObjectType#m-boundswidth) / [bounds](uiObjectType#m-bounds) ]

Alias of [UiSelector#boundsWidth](#boundswidthvalue).

### width(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for rectangle width (as absolute value or percentage)
- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for rectangle width (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The width of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsWidth](uiObjectType#m-boundswidth) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsWidth](#boundswidthmin-max)'s alias method.

## [m#] height

### height(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle height (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The height of the control's rectangle matches the specified measurement.
- Associated control property: [ [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsHeight](#boundsheightvalue)'s alias method.

### height(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for rectangle height (as absolute value or percentage)
- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for rectangle height (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The height of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsHeight](#boundsheightmin-max)'s alias method.

## [m#] centerX

### centerX(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Rectangle center point X coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The X coordinate of the center point of the control's rectangle matches the specified value.
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsCenterX](#boundscenterxvalue)'s alias method.

### centerX(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum center point X coordinate (as value or percentage)
- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum center point X coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The X coordinate of the center point of the control's rectangle matches the specified range.
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsCenterX](#boundscenterxmin-max)'s alias method.

## [m#] centerY

### centerY(value)

**`6.2.0`** **`Global`**

- **value** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Rectangle center point Y coordinate or percentage
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The Y coordinate of the center point of the control's rectangle matches the specified value.
- Associated control property: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsCenterY](#boundscenteryvalue)'s alias method.

### centerY(min, max)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum center point Y coordinate (as value or percentage)
- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum center point Y coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The Y coordinate of the center point of the control's rectangle matches the specified coordinate limit.
- Associated control properties: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsCenterY](#boundscenterymin-max)'s alias method.

## [m#] minLeft

### minLeft(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for the rectangle's left boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The left boundary of the control's rectangle matches the specified boundary limit.
- Associated control property: [ [boundsLeft](uiObjectType#m-boundsleft) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMinLeft](#boundsminleftmin)'s alias method.

## [m#] minTop

### minTop(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for the rectangle's top boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The top boundary of the control's rectangle matches the specified boundary limit
- Associated control property: [ [boundsTop](uiObjectType#m-boundstop) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMinTop](#boundsmintopmin)'s alias method.

## [m#] minRight

### minRight(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for the rectangle's right boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The right boundary of the control's rectangle matches the specified boundary range
- Associated control property: [ [boundsRight](uiObjectType#m-boundsright) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMinRight](#boundsminrightmin)'s alias method.

## [m#] minBottom

### minBottom(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for the rectangle's bottom boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The bottom boundary of the control's rectangle matches the specified boundary range.
- Associated control property: [ [boundsBottom](uiObjectType#m-boundsbottom) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMinBottom](#boundsminbottommin)'s alias method.

## [m#] minWidth

### minWidth(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum value for rectangle width (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The width of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsWidth](uiObjectType#m-boundswidth) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMinWidth](#boundsminwidthmin)'s alias method.

## [m#] minHeight

### minHeight(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum value for rectangle height (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The height of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMinHeight](#boundsminheightmin)'s alias method.

## [m#] minCenterX

### minCenterX(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Minimum center point X coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The X coordinate of the center point of the control's rectangle matches the specified range.
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMinCenterX](#boundsmincenterxmin)'s alias method.

## [m#] minCenterY

### minCenterY(min)

**`6.2.0`** **`Global`**

- **min** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Minimum center point Y coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The Y coordinate of the center point of the control's rectangle matches the specified coordinate limit.
- Associated control properties: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMinCenterY](#boundsmincenterymin)'s alias method.

## [m#] maxLeft

### maxLeft(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for the rectangle's left boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The left boundary of the control's rectangle matches the specified boundary limit.
- Associated control property: [ [boundsLeft](uiObjectType#m-boundsleft) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMaxLeft](#boundsmaxleftmax)'s alias method.

## [m#] maxTop

### maxTop(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for the rectangle's top boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The top boundary of the control's rectangle matches the specified boundary limit
- Associated control property: [ [boundsTop](uiObjectType#m-boundstop) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMaxTop](#boundsmaxtopmax)'s alias method.

## [m#] maxRight

### maxRight(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for the rectangle's right boundary (as X coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The right boundary of the control's rectangle matches the specified boundary range
- Associated control property: [ [boundsRight](uiObjectType#m-boundsright) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMaxRight](#boundsmaxrightmax)'s alias method.

## [m#] maxBottom

### maxBottom(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for the rectangle's bottom boundary (as Y coordinate or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The bottom boundary of the control's rectangle matches the specified boundary range.
- Associated control property: [ [boundsBottom](uiObjectType#m-boundsbottom) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMaxBottom](#boundsmaxbottommax)'s alias method.

## [m#] maxWidth

### maxWidth(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum value for rectangle width (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) size selector.

- Filtering condition: The width of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsWidth](uiObjectType#m-boundswidth) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMaxWidth](#boundsmaxwidthmax)'s alias method.

## [m#] maxHeight

### maxHeight(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum value for rectangle height (as absolute value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The height of the control's rectangle matches the specified metric limit.
- Associated control properties: [ [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMaxHeight](#boundsmaxheightmax)'s alias method.

## [m#] maxCenterX

### maxCenterX(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberX](dataTypes#screenmetricnumberx) } - Maximum center point X coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The X coordinate of the center point of the control's rectangle matches the specified range.
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMaxCenterX](#boundsmaxcenterxmax)'s alias method.

## [m#] maxCenterY

### maxCenterY(max)

**`6.2.0`** **`Global`**

- **max** { [ScreenMetricNumberY](dataTypes#screenmetricnumbery) } - Maximum center point Y coordinate (as value or percentage)
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) boundary selector.

- Filtering condition: The Y coordinate of the center point of the control's rectangle matches the specified coordinate limit.
- Associated control properties: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

[UiSelector#boundsMaxCenterY](#boundsmaxcenterymax)'s alias method.

## [m#] screenCenterX

### screenCenterX(b, tolerance)

**`6.2.0`** **`Global`**

- **b** { [boolean](dataTypes#boolean) } - Whether the X coordinate is centered
- **tolerance** { [number](dataTypes#number) } - Centering error tolerance
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: Whether the difference between the control's rectangle center point X coordinate and the screen center X coordinate is within the error tolerance matches the specified parameter (b).
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
device.width; // 1080

wA.bounds(); // Rect(520, 48 - 560, 160)
wA.boundsCenterX(); // 540
Math.abs(wA.boundsCenterX() - device.width / 2) / device.width; // 0

wB.bounds(); // Rect(50, 96 - 1040, 1280)
wB.boundsCenterX(); // 545
Math.abs(wB.boundsCenterX() - device.width / 2) / device.width; /* Approximately 0.005 . */

wC.bounds(); // Rect(66, 112 - 256, 1600)
wC.boundsCenterX(); // 161
Math.abs(wC.boundsCenterX() - device.width / 2) / device.width; /* Approximately 0.351 . */
```

`screenCenterX(true, 0)` is a control rectangle center point selector that can match control `wA`; the parameter `0` means strict horizontal centering with no error allowed, `true` means normal filtering, and if `false`, it means reverse filtering (i.e., select controls that do not satisfy strict horizontal centering).

`screenCenterX(true, 0.1)` is also a control rectangle center point selector that can match controls `wA` and `wB`, because `wA` is strictly horizontally centered, `wB`'s centering error is about `0.005`, which is less than the specified `0.1`, while `wC`'s centering error is too large and thus not selected.

[Pickup selector](#m-pickup) examples:

```js
pickup(screenCenterX(0.1), '@');
pickup({ screenCenterX: 0.1 }, '@');
```

### screenCenterX(b)

**`6.2.0`** **`Global`**

- **b** { [boolean](dataTypes#boolean) } - Whether the X coordinate is centered
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: Whether the difference between the control rectangle's center X coordinate and the screen center X coordinate is within the error tolerance matches the specified parameter (b).
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

Overload of [UiSelector#screenCenterX](#screencenterx)(`b`, `0.016`).

### screenCenterX(tolerance)

**`6.2.0`** **`Global`**

- **tolerance** { [number](dataTypes#number) } - Centering error tolerance
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The difference between the control rectangle's center X coordinate and the screen center X coordinate is within the error tolerance.
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

Overload of [UiSelector#screenCenterX](#screencenterx)(`true`, `tolerance`).

### screenCenterX()

**`6.2.0`** **`Global`**

- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The difference between the control rectangle's center point X coordinate and the screen center X coordinate is not greater than 0.016
- Associated control property: [ [boundsCenterX](uiObjectType#m-boundscenterx) / [bounds](uiObjectType#m-bounds) ]

Overload of [UiSelector#screenCenterX](#screencenterx)(`true`, `0.016`).

## [m#] screenCenterY

### screenCenterY(b, tolerance)

**`6.2.0`** **`Global`**

- **b** { [boolean](dataTypes#boolean) } - Whether the Y coordinate is centered
- **tolerance** { [number](dataTypes#number) } - Centering error tolerance
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: Whether the difference between the control's rectangle center point Y coordinate and the screen center Y coordinate is within the error tolerance matches the specified parameter (b).
- Associated control property: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 3 controls:

```js
device.height; // 1920

wA.bounds(); // Rect(10, 48 - 260, 1872)
wA.boundsCenterY(); // 960
Math.abs(wA.boundsCenterY() - device.width / 2) / device.width; // 0

wB.bounds(); // Rect(150, 96 - 1020, 1820)
wB.boundsCenterY(); // 958
Math.abs(wB.boundsCenterY() - device.width / 2) / device.width; /* Approximately 0.001 . */

wC.bounds(); // Rect(266, 1400 - 356, 1600)
wC.boundsCenterY(); // 1500
Math.abs(wC.boundsCenterY() - device.width / 2) / device.width; /* Approximately 0.281 . */
```

`screenCenterY(true, 0)` is a control rectangle center point selector that can match control `wA`; the parameter `0` means strict vertical centering with no error allowed, `true` means normal filtering, and if `false`, it means reverse filtering (i.e., select controls that do not satisfy strict vertical centering).

`screenCenterY(true, 0.1)` is also a control rectangle center point selector that can match controls `wA` and `wB`, because `wA` is strictly vertically centered, `wB`'s centering error is about `0.001`, which is less than the specified `0.1`, while `wC`'s centering error is too large and thus not selected.

[Pickup selector](#m-pickup) examples:

```js
pickup(screenCenterY(0.1), '@');
pickup({ screenCenterY: 0.1 }, '@');
```

### screenCenterY(b)

**`6.2.0`** **`Global`**

- **b** { [boolean](dataTypes#boolean) } - Whether the Y coordinate is centered
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: Whether the difference between the control rectangle's center point Y coordinate and the screen center Y coordinate is within the error tolerance matches the specified parameter (b)
- 关联控件属性: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

Overload of [UiSelector#screenCenterY](#screencentery)(`b`, `0.016`).

### screenCenterY(tolerance)

**`6.2.0`** **`Global`**

- **tolerance** { [number](dataTypes#number) } - Centering error tolerance
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The difference between the control's rectangle center point Y coordinate and the screen center Y coordinate is within the error tolerance.
- Associated control property: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

Overload of [UiSelector#screenCenterY](#screencentery)(`true`, `tolerance`).

### screenCenterY()

**`6.2.0`** **`Global`**

- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) center point selector.

- Filtering condition: The difference between the control's rectangle center point Y coordinate and the screen center Y coordinate is not greater than 0.016.
- Associated control property: [ [boundsCenterY](uiObjectType#m-boundscentery) / [bounds](uiObjectType#m-bounds) ]

Overload of [UiSelector#screenCenterY](#screencentery)(`true`, `0.016`).

## [m#] screenCoverage

### screenCoverage(min)

**`6.2.0`** **`Global`**

- **min** { [number](dataTypes#number) } - Minimum spatial occupancy ratio of the visible portion of the rectangle
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) spatial selector.

- Filtering condition: The spatial occupancy ratio of the visible portion of the control's rectangle (i.e., screen coverage) satisfies the specified parameter.
- Associated control property: [ [boundsWidth](uiObjectType#m-boundswidth) / [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

For example, for the following 5 controls:

```js
device.width; // 1080
device.height; // 1920

wA.bounds(); // Rect(0, 0 - 1080, 1896)
(wA.width() * wA.height()) / (device.width * device.height); // 0.9875

wB.bounds(); // Rect(150, 96 - 1020, 1820)
(wB.width() * wB.height()) / (device.width * device.height); /* Approximately 0.723 .*/

wC.bounds(); /* Rect(-2000, -1400 - 80, 1920), screen coverage approximately 7.4% . */
wD.bounds(); /* Rect(-200, 0 - 1080, 1920), screen coverage 100% . */
wE.bounds(); /* Rect(20, 30 - 840, 4000), screen coverage approximately 74.7% . */
```

`screenCoverage(0.95)` is a control rectangle spatial selector that can match controls `wA` and `wD`; the parameter `0.95` means the spatial occupancy of the visible portion is not less than `95%`. `wD` is special in that its left boundary is negative, meaning the left boundary extends beyond the visible screen area, so it is treated as `0` in calculations.

`wC` and `wE` are also special.  
`wC`'s left and top boundaries are both negative, extending beyond the visible screen area, so the area is treated as `0` in calculations:

```js
/* (right - left) * (bottom - top) */
(80 - 0) * (1920 - 0)
```

`wE`'s bottom boundary is `4000`, which is greater than the example device height `1920`, extending beyond the visible screen area, so the area is calculated using the device height `1920`:

```js
/* (right - left) * (bottom - top) */
(840 - 20) * (1920 - 30)
```

Therefore, among the 5 controls, `wC` has the lowest screen coverage. For the selector `screenCoverage(0.7)`, all 4 controls except `wC` can be selected.

[Pickup selector](#m-pickup) examples:

```js
pickup(screenCoverage(0.7), '@');
pickup({ screenCoverage: 0.7 }, '@');
```

### screenCoverage()

**`6.2.0`** **`Global`**

- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control rectangle (Rect)](androidRectType) spatial selector.

- Filtering condition: The screen occupancy ratio of the visible portion of the control's rectangle is not less than `94.8%`.
- Associated control property: [ [boundsWidth](uiObjectType#m-boundswidth) / [boundsHeight](uiObjectType#m-boundsheight) / [bounds](uiObjectType#m-bounds) ]

Overload of [UiSelector#screenCoverage](#screencoverage)(`0.948`).

## [m#] algorithm

### algorithm(str)

**`Global`**

- **str** { [string](dataTypes#string) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Algorithm configurator for the selector.

- Configurator description: Used to configure the traversal method used when retrieving window controls.
- Configuration options (case-insensitive):
    - `DFS` - Depth-First Search (default)
    - `BFS` - Breadth-First Search
- Associated control property: [ None ]

```js
console.log('DFS search time: ' +
    recorder(() => text('hi').algorithm('DFS').findOnce()));
console.log('BFS search time: ' +
    recorder(() => text('hi').algorithm('BFS').findOnce()));
```

BFS may improve some search efficiency when the control's [depth](uiObjectType#m-depth) is low or the total number of nodes in the [control hierarchy](glossaries#control-hierarchy) is small.

[Pickup selector](#m-pickup) examples:

```js
pickup(algorithm('BFS'), '@');
pickup({ algorithm: 'BFS' }, '@');
```

## [m#] action

### action(...actions)

**`6.2.0`** **`Global`**

- **actions** { [...](documentation#可变参数)[string](dataTypes#string)[[]](documentation#可变参数) } - Control action IDs
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

[Control Actions](uiObjectActionsType) selector.

- Filtering condition: The control supports all the specified action parameters.
- Associated control properties: [ [actionNames](uiObjectType#m-actionnames) / [hasAction](uiObjectType#m-hasaction) ]

A control may support multiple control actions, such as click, long click, set text, etc. Each action corresponds to a control action ID. For example, the ID for click is `ACTION_CLICK`, and the ID for set text is `ACTION_SET_TEXT`. For more control action IDs, see the `Action IDs` table in the [Control Node Actions](uiObjectActionsType) chapter.

`action('ACTION_SET_TEXT')` is a control action selector that requires the control to support setting text.

`action('ACTION_CLICK')` is also a control action selector that requires the control to support clicking.

The `'ACTION_'` prefix in the parameters can be omitted, i.e., `action('SET_TEXT')` is equivalent to `action('ACTION_SET_TEXT')`.

The action selector supports [variadic parameters](documentation#可变参数). The `action('SET_TEXT', 'CLICK')` selector requires the control to support both setting text and clicking at the same time.

[Pickup selector](#m-pickup) examples:

```js
pickup(action('SET_TEXT'), '@');
pickup({ action: 'SET_TEXT' }, '@');

pickup(action('SET_TEXT', 'CLICK'), '@');
pickup({ action: [ 'SET_TEXT', 'CLICK' ] }, '@');
```

## [m#] filter

### filter(f)

**`Global`**

- **f** { [(](dataTypes#function)w: [UiObject](uiObjectType)[)](dataTypes#function) [=>](dataTypes#function) [boolean](dataTypes#boolean) } - Filter function
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Filter selector. Uses the filter function directly as the test condition for control filtering.

- Filtering condition: The control passes the filter test condition.
- Associated control property: [ None ]

The filter selector is equivalent to a highly customizable condition selector. It enables more specific and requirement-tailored control filtering.

```js
filter(w => w.text().length >= 5); /* Filter controls whose text length is not less than 5. */
filter(w => w.top() < cY(0.5) && w.width() > cX(0.9)); /* Filter controls whose rectangle top boundary is in the upper half of the screen and width is greater than 90% of screen width. */
filter(w => w.childCount() >= 2); /* Filter controls that have at least 2 child nodes. */
```

[Pickup selector](#m-pickup) examples:

```js
pickup(filter(w => w.childCount() >= 2), '@');
pickup({ filter: w => w.childCount() >= 2 }, '@');
```

## [m#] hasChildren

### hasChildren(b?)

**`6.2.0`** **`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control child nodes existence state selector.

- Filtering condition: The control's child nodes existence state matches the specified parameter.
- Associated control properties: [ [hasChildren](uiObjectType#m-haschildren) / [childCount](uiObjectType#m-childcount) ]

For example, for the following control:

```js
/* Indicates the control has at least one child node, i.e., the control is not a leaf node. */
w.hasChildren(); // true
```

Both `hasChildren()` and `hasChildren(true)` can match control `w`.

The `hasChildren()` selector is equivalent to the `filter(w => w.childCount() > 0)` selector.

[Pickup selector](#m-pickup) examples:

```js
pickup(hasChildren(), '@');
pickup({ hasChildren: [] }, '@');
pickup({ hasChildren: null }, '@'); /* Not recommended. */

pickup(hasChildren(true), '@');
pickup({ hasChildren: true }, '@');
```

## [m#] checkable

### checkable(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control checkability selector.

- Filtering condition: The control's checkability matches the specified parameter.
- Associated control property: [checkable](uiObjectType#m-checkable)

For example, for the following control:

```js
/* Indicates the control can be checked/selected. */
w.checkable(); // true
```

`checkable()` and `checkable(true)` can both match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(checkable(), '@');
pickup({ checkable: [] }, '@');
pickup({ checkable: null }, '@'); /* Not recommended. */

pickup(checkable(true), '@');
pickup({ checkable: true }, '@');
```

## [m#] checked

### checked(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control checked state selector.

- Filtering condition: The control's checked state matches the specified parameter.
- Associated control property: [checked](uiObjectType#m-checked)

For example, for the following control:

```js
/* Indicates the control has been checked/selected. */
w.checked(); // true
```

Both `checked()` and `checked(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(checked(), '@');
pickup({ checked: [] }, '@');
pickup({ checked: null }, '@'); /* Not recommended. */

pickup(checked(true), '@');
pickup({ checked: true }, '@');
```

## [m#] focusable

### focusable(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control focusability selector.

- Filtering condition: The control's focusability matches the specified parameter.
- Associated control property: [focusable](uiObjectType#m-focusable)

For example, for the following control:

```js
/* Indicates the control can be focused. */
w.focusable(); // true
```

Both `focusable()` and `focusable(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(focusable(), '@');
pickup({ focusable: [] }, '@');
pickup({ focusable: null }, '@'); /* Not recommended. */

pickup(focusable(true), '@');
pickup({ focusable: true }, '@');
```

## [m#] focused

### focused(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control focused state selector.

- Filtering condition: The control's focused state matches the specified parameter.
- Associated control property: [focused](uiObjectType#m-focused)

For example, for the following control:

```js
/* Indicates the control has been focused. */
w.focused(); // true
```

Both `focused()` and `focused(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(focused(), '@');
pickup({ focused: [] }, '@');
pickup({ focused: null }, '@'); /* Not recommended. */

pickup(focused(true), '@');
pickup({ focused: true }, '@');
```

## [m#] visibleToUser

### visibleToUser(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control visibility to user state selector.

- Filtering condition: The control's visibility to user state matches the specified parameter.
- Associated control property: [visibleToUser](uiObjectType#m-visibletouser)

For example, for the following control:

```js
/* Indicates the control is visible to the user. */
w.visibleToUser(); // true
```

Both `visibleToUser()` and `visibleToUser(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(visibleToUser(), '@');
pickup({ visibleToUser: [] }, '@');
pickup({ visibleToUser: null }, '@'); /* Not recommended. */

pickup(visibleToUser(true), '@');
pickup({ visibleToUser: true }, '@');
```

## [m#] accessibilityFocused

### accessibilityFocused(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control accessibility focus state selector.

- Filtering condition: The control's accessibility focus state matches the specified parameter.
- Associated control property: [accessibilityFocused](uiObjectType#m-accessibilityfocused)

For example, for the following control:

```js
/* Indicates the control supports accessibility focus behavior. */
w.accessibilityFocused(); // true
```

Both `accessibilityFocused()` and `accessibilityFocused(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(accessibilityFocused(), '@');
pickup({ accessibilityFocused: [] }, '@');
pickup({ accessibilityFocused: null }, '@'); /* Not recommended. */

pickup(accessibilityFocused(true), '@');
pickup({ accessibilityFocused: true }, '@');
```

## [m#] selected

### selected(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control selected state selector.

- Filtering condition: The control's selected state matches the specified parameter.
- Associated control property: [selected](uiObjectType#m-selected)

For example, for the following control:

```js
/* Indicates the control supports selected behavior. */
w.selected(); // true
```

Both `selected()` and `selected(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(selected(), '@');
pickup({ selected: [] }, '@');
pickup({ selected: null }, '@'); /* Not recommended. */

pickup(selected(true), '@');
pickup({ selected: true }, '@');
```

## [m#] clickable

### clickable(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control clickability selector.

- Filtering condition: The control's clickability matches the specified parameter.
- Associated control property: [clickable](uiObjectType#m-clickable)

For example, for the following control:

```js
/* Indicates the control supports click behavior. */
w.clickable(); // true
```

`clickable()` and `clickable(true)` can both match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(clickable(), '@');
pickup({ clickable: [] }, '@');
pickup({ clickable: null }, '@'); /* Not recommended. */

pickup(clickable(true), '@');
pickup({ clickable: true }, '@');
```

## [m#] longClickable

### longClickable(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control long-clickability selector.

- Filtering condition: The control's long-clickability matches the specified parameter.
- Associated control property: [longClickable](uiObjectType#m-longclickable)

For example, for the following control:

```js
/* Indicates the control supports long click behavior. */
w.longClickable(); // true
```

`longClickable()` and `longClickable(true)` can both match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(longClickable(), '@');
pickup({ longClickable: [] }, '@');
pickup({ longClickable: null }, '@'); /* Not recommended. */

pickup(longClickable(true), '@');
pickup({ longClickable: true }, '@');
```

## [m#] enabled

### enabled(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control enabled state selector.

- Filtering condition: The control's enabled state matches the specified parameter.
- Associated control property: [enabled](uiObjectType#m-enabled)

For example, for the following control:

```js
/* Indicates the control is enabled (not disabled). */
w.enabled(); // true
```

`enabled()` and `enabled(true)` can both match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(enabled(), '@');
pickup({ enabled: [] }, '@');
pickup({ enabled: null }, '@'); /* Not recommended. */

pickup(enabled(true), '@');
pickup({ enabled: true }, '@');
```

## [m#] password

### password(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control password state selector.

- Filtering condition: The control's password state matches the specified parameter.
- Associated control property: [password](uiObjectType#m-password)

For example, for the following control:

```js
/* Indicates the control is a password control. */
w.password(); // true
```

Both `password()` and `password(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(password(), '@');
pickup({ password: [] }, '@');
pickup({ password: null }, '@'); /* Not recommended. */

pickup(password(true), '@');
pickup({ password: true }, '@');
```

## [m#] scrollable

### scrollable(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control scrollability selector.

- Filtering condition: The control's scrollability matches the specified parameter.
- Associated control property: [scrollable](uiObjectType#m-scrollable)

For example, for the following control:

```js
/* Indicates the control is scrollable. */
w.scrollable(); // true
```

Both `scrollable()` and `scrollable(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(scrollable(), '@');
pickup({ scrollable: [] }, '@');
pickup({ scrollable: null }, '@'); /* Not recommended. */

pickup(scrollable(true), '@');
pickup({ scrollable: true }, '@');
```

## [m#] editable

### editable(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control editability selector.

- Filtering condition: The control's editability matches the specified parameter.
- Associated control property: [editable](uiObjectType#m-editable)

For example, for the following control:

```js
/* Indicates the control is editable. */
w.editable(); // true
```

Both `editable()` and `editable(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(editable(), '@');
pickup({ editable: [] }, '@');
pickup({ editable: null }, '@'); /* Not recommended. */

pickup(editable(true), '@');
pickup({ editable: true }, '@');
```

## [m#] contentValid

### contentValid(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control content validity state selector.

- Filtering condition: The control's content validity state matches the specified parameter.
- Associated control property: isContentValid

For example, for the following control:

```js
/* Indicates the control has valid content. */
w.isContentValid(); // true
```

Both `contentValid()` and `contentValid(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(contentValid(), '@');
pickup({ contentValid: [] }, '@');
pickup({ contentValid: null }, '@'); /* Not recommended. */

pickup(contentValid(true), '@');
pickup({ contentValid: true }, '@');
```

## [m#] contextClickable

### contextClickable(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control context clickability selector.

- Filtering condition: The control's context clickability matches the specified parameter.
- Associated control property: isContextClickable

For example, for the following control:

```js
/* Indicates the control supports context click behavior. */
w.isContextClickable(); // true
```

Both `contextClickable()` and `contextClickable(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(contextClickable(), '@');
pickup({ contextClickable: [] }, '@');
pickup({ contextClickable: null }, '@'); /* Not recommended. */

pickup(contextClickable(true), '@');
pickup({ contextClickable: true }, '@');
```

## [m#] multiLine

### multiLine(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control multi-line text editability selector.

- Filtering condition: The control's multi-line text editability matches the specified parameter.
- Associated control property: isMultiLine

For example, for the following control:

```js
/* Indicates the control is text-editable and supports multi-line editing. */
w.isMultiLine(); // true
```

Both `multiLine()` and `multiLine(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(multiLine(), '@');
pickup({ multiLine: [] }, '@');
pickup({ multiLine: null }, '@'); /* Not recommended. */

pickup(multiLine(true), '@');
pickup({ multiLine: true }, '@');
```

## [m#] dismissable

### dismissable(b?)

**`Overload [1-2]/2`** **`Global`**

- **[ b = true ]** { [boolean](dataTypes#boolean) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control dismissability selector.

- Filtering condition: The control's dismissability matches the specified parameter.
- Associated control property: isDismissable

For example, for the following control:

```js
/* Indicates the control can be dismissed. */
w.isDismissable(); // true
```

Both `dismissable()` and `dismissable(true)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(dismissable(), '@');
pickup({ dismissable: [] }, '@');
pickup({ dismissable: null }, '@'); /* Not recommended. */

pickup(dismissable(true), '@');
pickup({ dismissable: true }, '@');
```

## [m#] depth

### depth(d)

**`Global`**

- **d** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control [hierarchy depth](glossaries#control-hierarchy) numeric selector.

- Filtering condition: The control's hierarchy depth matches the specified parameter.
- Associated control property: [depth](uiObjectType#m-depth)

For example, for the following control:

```js
w.depth(); // 5
```

`depth(5)` is a control numeric selector that can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(depth(5), '@');
pickup({ depth: 5 }, '@');
```

## [m#] rowCount

### rowCount(d)

**`Global`**

- **d** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control [collection info control](glossaries#collection-info-control) row count numeric selector.

- Filtering condition: The control's collection info control row count matches the specified parameter.
- Associated control property: [rowCount](uiObjectType#m-rowcount)

For example, for the following control:

```js
w.rowCount(); // 5
```

`rowCount(5)` is a control numeric selector that can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(rowCount(5), '@');
pickup({ rowCount: 5 }, '@');
```

## [m#] columnCount

### columnCount(d)

**`Global`**

- **d** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control column count numeric selector.

- Filtering condition: The control's column count matches the specified parameter.
- Associated control property: [columnCount](uiObjectType#m-columncount)

For example, for the following control:

```js
w.columnCount(); // 5
```

`columnCount(5)` is a control numeric selector that can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(columnCount(5), '@');
pickup({ columnCount: 5 }, '@');
```

## [m#] row

### row(d)

**`Global`**

- **d** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control [collection item info control](glossaries#collection-item-info-control) row index numeric selector.

- Filtering condition: The control's collection item info control row index matches the specified parameter.
- Associated control property: [row](uiObjectType#m-row)

For example, for the following control:

```js
w.row(); // 5
```

`row(5)` is a control numeric selector that can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(row(5), '@');
pickup({ row: 5 }, '@');
```

## [m#] column

### column(d)

**`Global`**

- **d** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control [collection item info control](glossaries#collection-item-info-control) column index numeric selector.

- Filtering condition: The control's collection item info control column index matches the specified parameter.
- Associated control property: [column](uiObjectType#m-column)

For example, for the following control:

```js
w.column(); // 5
```

`column(5)` is a control numeric selector that can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(column(5), '@');
pickup({ column: 5 }, '@');
```

## [m#] rowSpan

### rowSpan(d)

**`Global`**

- **d** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control [collection item info control](glossaries#collection-item-info-control) row span numeric selector.

- Filtering condition: The control's collection item info control row span matches the specified parameter.
- Associated control property: [rowSpan](uiObjectType#m-rowspan)

For example, for the following control:

```js
w.rowSpan(); // 5
```

`rowSpan(5)` is a control numeric selector that can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(rowSpan(5), '@');
pickup({ rowSpan: 5 }, '@');
```

## [m#] columnSpan

### columnSpan(d)

**`Global`**

- **d** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control [collection item info control](glossaries#collection-item-info-control) column span numeric selector.

- Filtering condition: The control's collection item info control column span matches the specified parameter.
- Associated control property: [columnSpan](uiObjectType#m-columnspan)

For example, for the following control:

```js
w.columnSpan(); // 5
```

`columnSpan(5)` is a control numeric selector that can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(columnSpan(5), '@');
pickup({ columnSpan: 5 }, '@');
```

## [m#] drawingOrder

### drawingOrder(order)

**`6.2.0`** **`Global`**

- **order** { [number](dataTypes#number) } - Control view drawing order
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control drawing order numeric selector.

- Filtering condition: The control's drawing order matches the specified parameter.
- Associated control property: [drawingOrder](uiObjectType#m-drawingorder)

For example, for the following control:

```js
w.drawingOrder(); // 23
```

`drawingOrder(23)` can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(drawingOrder(23), '@');
pickup({ drawingOrder: 23 }, '@');
```

## [m#] indexInParent

### indexInParent(d)

**`Global`**

- **d** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control index in parent numeric selector.

- Filtering condition: The control's index within its parent matches the specified parameter.
- Associated control property: [indexInParent](uiObjectType#m-indexinparent)

For example, for the following control:

```js
w.indexInParent(); // 5
```

`indexInParent(5)` is a control numeric selector that can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(indexInParent(5), '@');
pickup({ indexInParent: 5 }, '@');
```

## [m#] childCount

### childCount(d)

**`6.2.0`** **`Global`**

- **d** { [number](dataTypes#number) }
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control child count numeric selector.

- Filtering condition: The control's child count matches the specified parameter.
- Associated control property: [childCount](uiObjectType#m-childcount)

For example, for the following control:

```js
w.childCount(); // 5
```

`childCount(5)` is a control numeric selector that can match control `w`.

[Pickup selector](#m-pickup) examples:

```js
pickup(childCount(5), '@');
pickup({ childCount: 5 }, '@');
```

## [m#] minChildCount

### minChildCount(min)

**`6.2.0`** **`Global`**

- **min** { [number](dataTypes#number) } - Minimum number of child nodes for the control
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control child count numeric selector.

- Filtering condition: The control's child count matches the specified limit parameter.
- Associated control property: [childCount](uiObjectType#m-childcount)

For example, for the following controls:

```js
wA.childCount(); // 0
wB.childCount(); // 3
wC.childCount(); // 5
```

`minChildCount(2)` is a control numeric selector that can match controls `wB` and `wC`.

[Pickup selector](#m-pickup) examples:

```js
pickup(minChildCount(2), '@');
pickup({ minChildCount: 2 }, '@');
```

## [m#] maxChildCount

### maxChildCount(max)

**`6.2.0`** **`Global`**

- **max** { [number](dataTypes#number) } - Maximum number of child nodes for the control
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) }

Control child count numeric selector.

- Filtering condition: The control's child count matches the specified limit parameter.
- Associated control property: [childCount](uiObjectType#m-childcount)

For example, for the following controls:

```js
wA.childCount(); // 0
wB.childCount(); // 3
wC.childCount(); // 5
```

`maxChildCount(4)` is a control numeric selector that can match controls `wA` and `wB`.

[Pickup selector](#m-pickup) examples:

```js
pickup(maxChildCount(4), '@');
pickup({ maxChildCount: 4 }, '@');
```

## [m#] findOnce

### findOnce()

**`Global`** **`Overload 1/2`** **`A11Y`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Filter controls according to the selector conditions.  
The result is a single control. Returns null if no control matches the conditions.

Characteristics:

- Blocking filter - [ × ]
- Collection result - [ × ]

```js
let sel = text('hello').boundsCenterY(0.3);
let w = sel.findOnce();
```

In the example above, `w` represents the first control that matches the conditions (may be null).

### findOnce(index)

**`Global`** **`Overload 2/2`** **`A11Y`**

- **index** { [number](dataTypes#number) } - Control index
- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Filter controls according to the selector conditions.  
The result is the single control at the specified index. Returns null if none exists.

Characteristics:

- Blocking filter - [ × ]
- Collection result - [ × ]

```js
let sel = text('hello').boundsCenterY(0.3);
let wA = sel.findOnce();
let wB = sel.findOnce(0);
let wC = sel.findOnce(4);
```

In the example above, `wB` is equivalent to `wA`, representing the first (index 0) control that matches the conditions (may be null).  
`wC` represents the 5th control that matches the conditions (may be null).

## [m#] exists

### exists()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Determine whether there exists a control that satisfies the selector conditions.

Equivalent to `UiSelector#findOnce() !== null`.

## [m#] find

### find()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

Filter all controls that satisfy the selector conditions.  
The result is a [UiObjectCollection](uiObjectCollectionType). Returns an empty collection if no controls match.

Characteristics:

- Blocking filter - [ × ]
- Collection result - [ √ ]

```js
let sel = text('hello').boundsCenterY(0.3);
let wc = sel.find();
wc.forEach(w => console.log(w.centerY()));
```

In the example above, `wc` represents the collection of controls that match the conditions.

## [m#] findOne

### findOne(timeout)

**`Global`** **`Overload 1/2`** **`A11Y`** **`Non-UI`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Continuously filter controls according to the selector conditions until a matching control appears or the timeout is reached.  
The result is a single control. Returns null if no matching control is found within the specified timeout.

Characteristics:

- Blocking filter - [ √ ]
- Collection result - [ × ]

```js
let sel = text('hello').boundsCenterY(0.3);
let w = sel.findOne(3e3); /* 3000 milliseconds, i.e., 3 seconds. */
console.log(w.centerY());
```

In the example above, `w` represents the first control that matches the conditions within 3 seconds; null if timed out.

### findOne()

**`Global`** **`Overload 2/2`** **`A11Y`** **`Non-UI`** **`DEPRECATED`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) }

Continuously filter controls according to the selector conditions until a matching control appears.  
This may cause the script to **block permanently**.  
The result is a single control.

Characteristics:

- Blocking filter - [ √ ]
- Collection result - [ × ]

This method is equivalent to `UiSelector#findOne(-1)`.  
Because `findOne()` easily causes ambiguity and confusion, it is deprecated. It is recommended to use `findOne(-1)` or `untilFindOne()` instead.

```js
let sel = text('hello').boundsCenterY(0.3);
let w = sel.findOne();
console.log(w.centerY());
```

In the example above, `w` represents the first control that matches the conditions.  
The third line `console.log(w.centerY());` may never execute unless `sel.findOne()` succeeds in unblocking.

## [m#] untilFindOne

### untilFindOne()

**`Global`** **`A11Y`** **`Non-UI`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) }

Continuously filter controls according to the selector conditions until a matching control appears.  
This may cause the script to **block permanently**.  
The result is a single control.

Characteristics:

- Blocking filter - [ √ ]
- Collection result - [ × ]

This method is equivalent to `UiSelector#findOne(-1)`.

```js
let sel = text('hello').boundsCenterY(0.3);
let w = sel.untilFindOne();
console.log(w.centerY());
```

In the example above, `w` represents the first control that matches the conditions.  
The third line `console.log(w.centerY());` may never execute unless `sel.untilFindOne()` succeeds in unblocking.

## [m#] untilFind

### untilFind()

**`Global`** **`A11Y`** **`Non-UI`**

- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

Continuously filter controls according to the selector conditions until a matching control appears.  
This may cause the script to **block permanently**.  
The result is a control collection.

Characteristics:

- Blocking filter - [ √ ]
- Collection result - [ √ ]

```js
let sel = text('hello').boundsCenterY(0.3);
let wc = sel.untilFind();
console.log(wc.length);
```

In the example above, `wc` represents the collection of controls that match the conditions.  
The third line `console.log(wc.length);` may never execute unless `sel.untilFind()` succeeds in unblocking.

## [m#] waitFor

### waitFor()

**`Global`** **`A11Y`** **`Non-UI`** **`DEPRECATED`**

- <ins>**returns**</ins> { [UiObjectCollection](uiObjectCollectionType) }

Continuously filter controls according to the selector conditions until a matching control appears.  
This may cause the script to **block permanently**.  
The result is a control collection.

Characteristics:

- Blocking filter - [ √ ]
- Collection result - [ √ ]

Alias of [UiSelector#untilFind](#untilfind).

Because `waitFor()` easily causes ambiguity and confusion, it is deprecated. It is recommended to use `untilFind()` instead.

## [m#] performAction

Used to perform the specified control action.  
The relevant content has been described in detail in the [Control Node Actions](uiObjectActionsType) chapter. Only the method signature is noted here; the related content will not be repeated.

### performAction(action, ...arguments)

**`Global`** **`A11Y`**

- **action** { [number](dataTypes#number) } - Unique identifier of the action (Action ID)
- **arguments** { [...](documentation#可变参数)[ActionArgument](uiObjectActionsType#i-actionargument)[[]](documentation#可变参数) } - Action arguments, used to pass parameters to the action
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been executed without exceptions during execution

## [m#] click

### click()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ click ] action](uiObjectActionsType#m-click) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions), this method is not recommended.

> Note: This method is not global; it is replaced by automator.click.

## [m#] longClick

### longClick()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ long click ] action](uiObjectActionsType#m-longclick) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions), this method is not recommended.

> Note: This method is not global; it is replaced by automator.longClick.

## [m#] accessibilityFocus

### accessibilityFocus()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ accessibility focus ] action](uiObjectActionsType#m-accessibilityfocus) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] clearAccessibilityFocus

### clearAccessibilityFocus()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ clear accessibility focus ] action](uiObjectActionsType#m-clearaccessibilityfocus) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] focus

### focus()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ focus ] action](uiObjectActionsType#m-focus) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] clearFocus

### clearFocus()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ clear focus ] action](uiObjectActionsType#m-clearfocus) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] dragStart

### dragStart()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ drag start ] action](uiObjectActionsType#m-dragstart) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] dragDrop

### dragDrop()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ drag drop ] action](uiObjectActionsType#m-dragdrop) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] dragCancel

### dragCancel()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=32`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ drag cancel ] action](uiObjectActionsType#m-dragcancel) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] imeEnter

### imeEnter()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=30`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ input method ENTER key ] action](uiObjectActionsType#m-imeenter) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] moveWindow

### moveWindow(x, y)

**`6.2.0`** **`Global`** **`A11Y`** **`API>=26`**

- **x** { [number](dataTypes#number) } - X coordinate
- **y** { [number](dataTypes#number) } - Y coordinate
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ move window to new position ] action](uiObjectActionsType#m-movewindow) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] nextAtMovementGranularity

### nextAtMovementGranularity(granularity, isExtendSelection)

**`6.2.0`** **`Global`** **`A11Y`**

- **granularity** { [number](dataTypes#number) } - Granularity
- **isExtendSelection** { [boolean](dataTypes#boolean) } - Whether to extend text selection
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ move to next position at granularity ] action](uiObjectActionsType#m-nextatmovementgranularity) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] nextHtmlElement

### nextHtmlElement(element)

**`6.2.0`** **`Global`** **`A11Y`**

- **element** { [string](dataTypes#string) } - Element name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ move to next element ] action](uiObjectActionsType#m-nexthtmlelement) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] pageLeft

### pageLeft()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ page left to move viewport ] action](uiObjectActionsType#m-pageleft) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] pageUp

### pageUp()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ page up to move viewport ] action](uiObjectActionsType#m-pageup) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] pageRight

### pageRight()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ page right to move viewport ] action](uiObjectActionsType#m-pageright) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] pageDown

### pageDown()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=29`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ page down to move viewport ] action](uiObjectActionsType#m-pagedown) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] pressAndHold

### pressAndHold()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=30`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ press and hold ] action](uiObjectActionsType#m-pressandhold) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] previousAtMovementGranularity

### previousAtMovementGranularity(granularity, isExtendSelection)

**`6.2.0`** **`Global`** **`A11Y`**

- **granularity** { [number](dataTypes#number) } - Granularity
- **isExtendSelection** { [boolean](dataTypes#boolean) } - Whether to extend text selection
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ move to previous position at granularity ] action](uiObjectActionsType#m-previousatmovementgranularity) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] previousHtmlElement

### previousHtmlElement(element)

**`6.2.0`** **`Global`** **`A11Y`**

- **element** { [string](dataTypes#string) } - Element name
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ move to previous element ] action](uiObjectActionsType#m-previoushtmlelement) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] showTextSuggestions

### showTextSuggestions()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=33`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ show text suggestions ] action](uiObjectActionsType#m-showtextsuggestions) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] showTooltip

### showTooltip()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=28`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ show tooltip information ] action](uiObjectActionsType#m-showtooltip) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] hideTooltip

### hideTooltip()

**`6.2.0`** **`Global`** **`A11Y`** **`API>=28`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ hide tooltip information ] action](uiObjectActionsType#m-hidetooltip) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] show

### show()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ show in viewport ] action](uiObjectActionsType#m-show) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] dismiss

### dismiss()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ dismiss ] action](uiObjectActionsType#m-dismiss) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] copy

### copy()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ copy text ] action](uiObjectActionsType#m-copy) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] cut

### cut()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ cut text ] action](uiObjectActionsType#m-cut) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] paste

### paste()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ paste text ] action](uiObjectActionsType#m-paste) on the collection.

When using the global method `paste()`, it is equivalent to `untilFind().paste()`. Since there is no filter condition before `untilFind()`, `untilFind()` will obtain the collection of all controls in the window, and every control in the collection will execute `paste()` once.  
However, when the global method `paste()` is actually executed, usually only one control performs the paste action — not every control executes it.  
This is because the prerequisite for control `w` to complete the paste action is that it must be in the focused state (`w.focused()` is `true`).  
In an active window, there is usually at most one control in the focused state, so only that control can complete the paste action.  
If you need all text editing controls to complete the paste action, refer to the following code:

```js 
let wc = className('EditText').find();
wc.forEach((w) => {
    w.focus();
    w.paste();
});
wc.at(-1).clearFocus();
```

Besides `w.paste()`, `w.setText(getClip())` can also be used to achieve the paste effect:

```js
className('EditText').find().forEach(w => w.setText(getClip()));
```

Unlike `w.paste()`, `w.setText()` does not require control `w` to be in the focused state.

Perform paste on a focused text editing control:

```js
focused().className('EditText').find().forEach(w => w.setText(getClip()));

/* 拾取器写法, 效果同上. */
pickup({
    focused: true,
    className: 'EditText',
}, '[w]').forEach(w => w.setText(getClip()));
```

Although the above example uses collection filtering, the obtained control collection usually contains only one control.

## [m#] select

### select()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ select ] action](uiObjectActionsType#m-select) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] expand

### expand()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ expand ] action](uiObjectActionsType#m-expand) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] collapse

### collapse()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ collapse ] action](uiObjectActionsType#m-collapse) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] scrollLeft

### scrollLeft()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ scroll to move viewport left ] action](uiObjectActionsType#m-scrollleft) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] scrollUp

### scrollUp()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ scroll to move viewport up ] action](uiObjectActionsType#m-scrollup) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions), this method is not recommended.

> Note: This method is not global; it is replaced by automator.scrollUp.

## [m#] scrollRight

### scrollRight()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ scroll to move viewport right ] action](uiObjectActionsType#m-scrollright) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] scrollDown

### scrollDown()

**`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ scroll to move viewport down ] action](uiObjectActionsType#m-scrolldown) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions), this method is not recommended.

> Note: This method is not global; it is replaced by automator.scrollDown.

## [m#] scrollForward

### scrollForward()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ scroll to move viewport forward ] action](uiObjectActionsType#m-scrollforward) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] scrollBackward

### scrollBackward()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ scroll to move viewport backward ] action](uiObjectActionsType#m-scrollbackward) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] scrollTo

### scrollTo(row, column)

**`Global`** **`A11Y`**

- **row** { [number](dataTypes#number) } - Row ordinal
- **column** { [number](dataTypes#number) } - Column ordinal
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ scroll specified position into viewport ] action](uiObjectActionsType#m-scrollto) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] contextClick

### contextClick()

**`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ context click ] action](uiObjectActionsType#m-contextclick) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] setText

### setText(text)

**`A11Y`**

- **text** { [string](dataTypes#string) } - Text
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ set text ] action](uiObjectActionsType#m-settext) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions), this method is not recommended.

> Note: This method is not global; it is replaced by automator.setText.

## [m#] setSelection

### setSelection(start, end)

**`Global`** **`A11Y`**

- **start** { [number](dataTypes#number) } - Start position
- **end** { [number](dataTypes#number) } - End position
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ select text ] action](uiObjectActionsType#m-setselection) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] clearSelection

### clearSelection()

**`6.2.0`** **`Global`** **`A11Y`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ clear text selection ] action](uiObjectActionsType#m-clearselection) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] setProgress

### setProgress(progress)

**`Global`** **`A11Y`**

- **progress** { [number](dataTypes#number) } - Progress value
- <ins>**returns**</ins> { [boolean](dataTypes#boolean) } - Whether the action has been fully executed without exceptions during execution.

According to the selector conditions, use [untilFind](#m-untilfind) to obtain a control collection, then perform the [[ set progress value ] action](uiObjectActionsType#m-setprogress) on the collection.

Due to the potential permanent blocking risk of [selector actions](#selector-actions) and the lack of targeting in global actions, this method is not recommended.

## [m#] plus

### plus(selector)

**`6.5.0`**

- **selector** { [UiSelector](uiSelectorType) } - Selector to be concatenated
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) } - The new concatenated selector

Selector concatenation without modifying the original selector.

```js
let selA = text('A').minTop(0.5);
let selB = desc('B').maxHeight(0.5);
let selPlused = selA.plus(selB);
console.log(selPlused); // text("A").minTop(0.5).desc("B").maxHeight(0.5)
console.log(selA); // text("A").minTop(0.5)
```

The example above shows that the `plus` method does not change the value of `selA`.

> See also: [append](#m-append) section.

## [m#] append

### append(selector)

**`6.5.0`**

- **selector** { [UiSelector](uiSelectorType) } - Selector to be concatenated
- <ins>**returns**</ins> { [UiSelector](uiSelectorType) } - The new concatenated selector

Selector concatenation that also modifies the original selector. This is a `mutable method`.

```js
let selA = text('A').minTop(0.5);
let selB = desc('B').maxHeight(0.5);
let selPlused = selA.append(selB);
console.log(selPlused); // text("A").minTop(0.5).desc("B").maxHeight(0.5)
console.log(selA); // text("A").minTop(0.5).desc("B").maxHeight(0.5)
```

The example above shows that the `append` method changes the value of `selA`.

Therefore, the above example is equivalent to the following:

```js
let selA = text('A').minTop(0.5);
let selB = desc('B').maxHeight(0.5);
selA.append(selB);
console.log(selA); // text("A").minTop(0.5).desc("B").maxHeight(0.5)
```

> See also: [plus](#m-plus) section.

## [m] pickup

Pickup selector (also called "picker") is a highly encapsulated mixed-form selector used for quick operations during control filtering and result processing.  
It supports [ mixed selector formats / control compass / result filtering / parameterized calls ], etc.

Some characteristics:

- `pickup` has been globalized and supports global usage.
- `pickup` supports [UiObject](uiObjectType) type parameters, but only uses them as the root node for control filtering; it cannot perform compass navigation or result filtering on them.
- The internal implementation of `pickup` references the [detect](uiObjectType#m-detect) method.

### pickup()

**`6.2.0`** **`Global`** **`Overload 1/17`** **`A11Y`**

- <ins>**returns**</ins> { [UiObject](uiObjectType) | [null](dataTypes#null) }

Unconditional picker, equivalent to `findOnce()`. The control obtained at this point is usually the one with [depth](uiObjectType#m-depth) `0` in the active window.

```js
pickup().depth(); // 0
```

### pickup(selector)

**`6.2.0`** **`Global`** **`Overload 2/17`** **`A11Y`**

- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector argument
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Equivalent to `selector.findOnce()`.

The `selector` parameter supports [single-type selectors](dataTypes#single-type-selector) ([classic selectors](dataTypes#classic-selector) / [content selectors](dataTypes#content-selector) / [object selectors](dataTypes#object-selector)) and [mixed-type selectors](dataTypes#mixed-type-selector):

```js
/* Classic selector argument. */
let selClassic = text('abc').clickable().centerX(0.5).boundsInside(0.2, 0.05, -1, -1).action('CLICK', 'SET_TEXT', 'LONG_CLICK');
pickup(selClassic);

/* Object selector argument. */
let selObject = {
    text: 'abc',
    clickable: [], /* or clickable: true */
    centerX: 0.5,
    boundsInside: [ 0.2, 0.05, -1, -1 ],
    action: [ 'CLICK', 'SET_TEXT', 'LONG_CLICK' ],
};
pickup(selObject);

/* Mixed-type selector argument. */
pickup([ 'abc', {
    clickable: [], /* or clickable: true */
    centerX: 0.5,
    boundsInside: [ 0.2, 0.05, -1, -1 ],
    action: [ 'CLICK', 'SET_TEXT', 'LONG_CLICK' ],
} ]);
```

### pickup(selector, result)

**`6.2.0`** **`Global`** **`Overload 3/17`** **`A11Y`**

- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **result** { [PickupResult](dataTypes#pickupresult) } - Result filtering parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Perform [result filtering](dataTypes#pickupresult) or [parameterized invocation](dataTypes#uiobjectinvokable) on `selector.findOnce()` according to the `result` parameter.

```js
/* Result filtering - text. */

pickup(textMatch(/ab?.+/), 'text'); /* Returns the text of the control that matches the filter condition. Returns empty string ("") if no matching control. */

/* Result filtering - point. */

pickup(clickable(true), 'point'); /* Returns the coordinates of the control that matches the filter condition. Returns null if no matching control. */
pickup(clickable(true), '.'); /* Same as above. */

/* Parameterized call - get control rectangle (Rect). */

pickup(clickable(true), 'bounds'); /* Null-pointer safe. */
clickable(true).findOnce().bounds(); /* Same effect as above, but potential null-pointer exception exists. */

/* Parameterized call - set text. */

pickup(className('EditText'), [ 'setText', 'hello' ]); /* Null-pointer safe. */
className('EditText').findOnce().setText('hello'); /* Same effect as above, but potential null-pointer exception exists. */

/* Parameterized call - set text selection. */

pickup(className('EditText'), [ 'setSelection', 1, 5 ]); /* Null-pointer safe. */
className('EditText').findOnce().setSelection(1, 5); /* Same effect as above, but potential null-pointer exception exists. */
```

### pickup(selector, compass)

**`6.2.0`** **`Global`** **`Overload 4/17`** **`A11Y`**

- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Control compass parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Perform [compass positioning](uiObjectType#m-compass) on `selector.findOnce()`.

```js
pickup(text('abc'), 'p3'); /* Null-pointer safe. */
text('abc').findOnce().parent().parent().parent(); /* Same effect as above, but potential null-pointer exception exists. */
```

### pickup(selector, compass, result)

**`6.2.0`** **`Global`** **`Overload 5/17`** **`A11Y`**

- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Control compass parameter
- **result** { [PickupResult](dataTypes#pickupresult) } - Result filtering parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

After performing [compass positioning](uiObjectType#m-compass) on `selector.findOnce()`, then perform [result filtering](dataTypes#pickupresult) or [parameterized invocation](dataTypes#uiobjectinvokable).

```js
pickup(text('abc'), 'p3', 'click'); /* Null-pointer safe. */
text('abc').findOnce().parent().parent().parent().click(); /* Same effect as above, but potential null-pointer exception exists. */

pickup(text('abc'), 's>1', 'bounds'); /* Null-pointer safe. */
let w = text('abc').findOnce();
w.parent().child(w.indexInParent() + 1).bounds(); /* Same effect as above, but potential null-pointer exception exists. */
```

### pickup(root, selector)

**`6.2.0`** **`Global`** **`Overload 6/17`** **`A11Y`**

- **root** { [UiObject](uiObjectType) } - Filter root node parameter
- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Use the control specified by the `root` parameter as the root node to perform `selector.findOnce()` filtering.

```js
let w = text('abc').findOnce();
pickup(w, 'xyz'); /* Filter for controls with content 'xyz' among all descendant nodes of control w. */
```

> See also: [pickup(selector)](#pickupselector)

### pickup(root, selector, result)

**`6.2.0`** **`Global`** **`Overload 7/17`** **`A11Y`**

- **root** { [UiObject](uiObjectType) } - Filter root node parameter
- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **result** { [PickupResult](dataTypes#pickupresult) } - Result filtering parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Use the control specified by the `root` parameter as the root node to perform [result filtering](dataTypes#pickupresult) or [parameterized invocation](dataTypes#uiobjectinvokable) on `selector.findOnce()` according to the `result` parameter.

```js
let w = text('abc').findOnce();
pickup(w, 'xyz', 'height'); /* Filter the height of the control with content 'xyz' among all descendant nodes of control w. */
```

> See also: [pickup(selector, result)](#pickupselector-result)

### pickup(root, selector, compass)

**`6.2.0`** **`Global`** **`Overload 8/17`** **`A11Y`**

- **root** { [UiObject](uiObjectType) } - Filter root node parameter
- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Control compass parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Use the control specified by the `root` parameter as the root node to perform [compass positioning](uiObjectType#m-compass) on `selector.findOnce()`.

```js
let w = text('abc').findOnce();
pickup(w, 'xyz', 'p2'); /* Filter the second-level parent node of the control with content 'xyz' among all descendant nodes of control w. */
```

> See also: [pickup(selector, compass)](#pickupselector-compass)

### pickup(root, selector, compass, result)

**`6.2.0`** **`Global`** **`Overload 9/17`** **`A11Y`**

- **root** { [UiObject](uiObjectType) } - Filter root node parameter
- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Control compass parameter
- **result** { [PickupResult](dataTypes#pickupresult) } - Result filtering parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Use the control specified by the `root` parameter as the root node to perform [compass positioning](uiObjectType#m-compass) on `selector.findOnce()`, then perform [result filtering](dataTypes#pickupresult) or [parameterized invocation](dataTypes#uiobjectinvokable).

```js
let w = text('abc').findOnce();
pickup(w, 'xyz', 'p2', 'width'); /* Filter the width of the second-level parent node of the control with content 'xyz' among all descendant nodes of control w. */
```

> See also: [pickup(selector, compass, result)](#pickupselector-compass-result)

### pickup(selector, callback)

**`6.2.0`** **`Global`** **`Overload 10/17`** **`A11Y`**

- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **callback** { [(](dataTypes#function)o: [any](dataTypes#any)[)](dataTypes#function) [=>](dataTypes#function) [R](dataTypes#generic) } - Filtering callback parameter
- <ins>**returns**</ins> { [R](dataTypes#generic) }

Add callback processing to [pickup(selector)](#pickupselector). The return value of the callback function (except `undefined`) is used as the final result. When the callback function returns `undefined`, the pickup result is used as the final result.

```js
pickup(text('abc'), (o) => {
    if (o !== null) {
        console.log(`Found the required control, its text is ${o.text()}`);
        return o.text();
    } else {
        console.warn(`Required control not found`);
        return '';
    }
}); /* The result of pickup may be the required control text or an empty string. */
```

### pickup(selector, result, callback)

**`6.2.0`** **`Global`** **`Overload 11/17`** **`A11Y`**

- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **result** { [PickupResult](dataTypes#pickupresult) } - Result filtering parameter
- **callback** { [(](dataTypes#function)o: [any](dataTypes#any)[)](dataTypes#function) [=>](dataTypes#function) [R](dataTypes#generic) } - Filtering callback parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Add callback processing to [pickup(selector, result)](#pickupselector-result). The return value of the callback function (except `undefined`) is used as the final result. When the callback function returns `undefined`, the pickup result is used as the final result.

```js
pickup(clickable(true), 'point', (o) => {
    if (o !== null) {
        console.log(`Found control, its center is at coordinate ${o}`);
        return o;
    }
    return org.opencv.core.Point();
}); /* pickup returns the control's real coordinate point or coordinate point (0, 0). */
```

### pickup(selector, compass, callback)

**`6.2.0`** **`Global`** **`Overload 12/17`** **`A11Y`**

- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Control compass parameter
- **callback** { [(](dataTypes#function)o: [any](dataTypes#any)[)](dataTypes#function) [=>](dataTypes#function) [R](dataTypes#generic) } - Filtering callback parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Add callback processing to [pickup(selector, compass)](#pickupselector-compass). The return value of the callback function (except `undefined`) is used as the final result. When the callback function returns `undefined`, the pickup result is used as the final result.

```js
pickup(text('abc'), 'p3', (o) => {
    if (o !== null && o.childCount() > 0) {
        o.children().forEach(w => w.setText('hello'));
    }
}); /* The result of pickup is the original pickup result. */
```

### pickup(selector, compass, result, callback)

**`6.2.0`** **`Global`** **`Overload 13/17`** **`A11Y`**

- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Control compass parameter
- **result** { [PickupResult](dataTypes#pickupresult) } - Result filtering parameter
- **callback** { [(](dataTypes#function)o: [any](dataTypes#any)[)](dataTypes#function) [=>](dataTypes#function) [R](dataTypes#generic) } - Filtering callback parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Add callback processing to [pickup(selector, compass, result)](#pickupselector-compass-result) using the control specified by the `root` parameter as the root node. The return value of the callback function (except `undefined`) is used as the final result. When the callback function returns `undefined`, the pickup result is used as the final result.

### pickup(root, selector, callback)

**`6.2.0`** **`Global`** **`Overload 14/17`** **`A11Y`**

- **root** { [UiObject](uiObjectType) } - Filter root node parameter
- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **callback** { [(](dataTypes#function)o: [any](dataTypes#any)[)](dataTypes#function) [=>](dataTypes#function) [R](dataTypes#generic) } - Filtering callback parameter
- <ins>**returns**</ins> { [R](dataTypes#generic) }

Add callback processing to [pickup(selector)](#pickupselector) using the control specified by the `root` parameter as the root node. The return value of the callback function (except `undefined`) is used as the final result. When the callback function returns `undefined`, the pickup result is used as the final result.

```js
/* w will be used as the root node. */
/* Can also be replaced with pickup({descMatch: /hello?.+/}). */
let w = descMatch(/hello?.+/).findOnce();

pickup(w, text('abc'), (o) => {
    if (o !== null) {
        console.log(`Found the required control, its text is ${o.text()}`);
        return o.text();
    } else {
        console.warn(`Required control not found`);
        return '';
    }
}); /* The result of pickup may be the required control text or an empty string. */
```

### pickup(root, selector, result, callback)

**`6.2.0`** **`Global`** **`Overload 15/17`** **`A11Y`**

- **root** { [UiObject](uiObjectType) } - Filter root node parameter
- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **result** { [PickupResult](dataTypes#pickupresult) } - Result filtering parameter
- **callback** { [(](dataTypes#function)o: [any](dataTypes#any)[)](dataTypes#function) [=>](dataTypes#function) [R](dataTypes#generic) } - Filtering callback parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Add callback processing to [pickup(selector, result)](#pickupselector-result) using the control specified by the `root` parameter as the root node. The return value of the callback function (except `undefined`) is used as the final result. When the callback function returns `undefined`, the pickup result is used as the final result.

```js
/* w will be used as the root node. */
/* Can also be replaced with pickup({descMatch: /hello?.+/}). */
let w = descMatch(/hello?.+/).findOnce();

pickup(w, clickable(true), 'point', (o) => {
    if (o !== null) {
        console.log(`Found control, its center is at coordinate ${o}`);
        return o;
    }
    return org.opencv.core.Point();
}); /* pickup returns the control's real coordinate point or coordinate point (0, 0). */
```

### pickup(root, selector, compass, callback)

**`6.2.0`** **`Global`** **`Overload 16/17`** **`A11Y`**

- **root** { [UiObject](uiObjectType) } - Filter root node parameter
- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Control compass parameter
- **callback** { [(](dataTypes#function)o: [any](dataTypes#any)[)](dataTypes#function) [=>](dataTypes#function) [R](dataTypes#generic) } - Filtering callback parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Add callback processing to [pickup(selector, compass)](#pickupselector-compass) using the control specified by the `root` parameter as the root node. The return value of the callback function (except `undefined`) is used as the final result. When the callback function returns `undefined`, the pickup result is used as the final result.

```js
/* w will be used as the root node. */
/* Can also be replaced with pickup({descMatch: /hello?.+/}). */
let w = descMatch(/hello?.+/).findOnce();

pickup(w, text('abc'), 'p3', (o) => {
    if (o !== null && o.childCount() > 0) {
        o.children().forEach(w => w.setText('hello'));
    }
}); /* The result of pickup is the original pickup result. */
```

### pickup(root, selector, compass, result, callback)

**`6.2.0`** **`Global`** **`Overload 17/17`** **`A11Y`**

- **root** { [UiObject](uiObjectType) } - Filter root node parameter
- **selector** { [PickupSelector](dataTypes#pickupselector) } - Mixed selector parameter
- **compass** { [DetectCompass](dataTypes#detectcompass) } - Control compass parameter
- **result** { [PickupResult](dataTypes#pickupresult) } - Result filtering parameter
- **callback** { [(](dataTypes#function)o: [any](dataTypes#any)[)](dataTypes#function) [=>](dataTypes#function) [R](dataTypes#generic) } - Filtering callback parameter
- <ins>**returns**</ins> { [any](dataTypes#any) } - Filtering result

Add callback processing to [pickup(selector, compass, result)](#pickupselector-compass-result) using the control specified by the `root` parameter as the root node. The return value of the callback function (except `undefined`) is used as the final result. When the callback function returns `undefined`, the pickup result is used as the final result.

```js
/* w 将作为根节点. */
/* 也可使用 pickup({descMatch: /hello?.+/}) 替换. */
let w = descMatch(/hello?.+/).findOnce();

pickup(w, text('abc'), 's>1', 'bounds', (o) => {
    if (o === null) {
        throw Error('Failed to obtain control rectangle. Please ensure the foreground page meets the requirements.');
    }
}); /* If no exception occurs, the result of pickup is the original pickup result. */
```

---

# Selector Actions

When performing control actions normally, the following process is used:

```text
Build selector - Filter (find) - Execute action on the result (control or collection)
```

The process for selector actions:

```text
Build selector - Execute action
```

## Execution Principle

Selector actions implicitly use the default filter process, which is [untilFind](#m-untilfind).

For example, `text('abc').click()` is equivalent to `text('abc').untilFind().click()`.

## Use with Caution

Global methods related to selector actions are not recommended for the following reasons.

1. **Potential permanent blocking risk**

   Because the `untilFind` method has blocking characteristics, it may cause the script to **block permanently**.  
   As in the example above, when `text('abc')` does not exist, the script will continue blocking.

2. **Global actions lack targeting**

   Take `paste()` as an example.  
   When using the global method `paste()`, it is equivalent to `untilFind().paste()`. Since there is no filter condition before `untilFind()`, it will obtain the collection of all controls in the window.  
   Such a collection often contains dozens or even hundreds of controls. When `paste()` is executed, every control in the collection performs `paste()` once.  
   Such operations are often unexpected and time-consuming. Therefore, it is not recommended to use global methods like `paste()`. It is recommended to use specific and controllable selectors to filter out particular controls or collections, and then perform the `paste()` operation in a targeted manner.

---

# Filter Types

## xxxStartsWith

Prefix matching filter.

The filter condition is of type [string](dataTypes#string) and matches the prefix of the corresponding control property string value.

```js
w.desc(); // splendid
descStartsWith('spl'); /* Can match w. */
descStartsWith('spa'); /* Cannot match w. */
```

## xxxEndsWith

Suffix matching filter.

The filter condition is of type [string](dataTypes#string) and matches the suffix of the corresponding control property string value.

```js
w.desc(); // splendid
descEndsWith('did'); /* Can match w. */
descEndsWith('diy'); /* Cannot match w. */
```

## xxxContains

Contains matching filter.

The filter condition is of type [string](dataTypes#string) and matches any length of consecutive characters in the control property string value.

```js
w.desc(); // splendid
descContains('did'); /* Can match w. */
descContains('spl'); /* Can match w. */
descContains('len'); /* Can match w. */
descContains(''); /* Can match w, but usually has no practical meaning. */
descContains('app'); /* Cannot match w. */
```

## xxxMatches

Regular expression full-match filter.

The filter condition is of type [string](dataTypes#string) or [RegExp](dataTypes#regexp) and fully matches the control property string value according to regular expression rules.

### Regular Expression Type

When the filter condition is a regular expression type, the effect is equivalent to JavaScript's [RegExp.prototype.test](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test), but it performs a full match from start to end, equivalent to automatically adding `^` at the start and `$` at the end of the match.

```js
w.desc(); // splendid
/* Equivalent to descMatch(/^s.*did$/) . */
descMatches(/s.*did/); /* Cannot match w. */
/* Equivalent to descMatch(/^did$/) . */
descMatches(/did/); /* Cannot match w. */
/* Equivalent to descMatch(/^did$/) . */
descMatches(/did$/); /* Cannot match w. */
/* Equivalent to descMatch(/^did$/) . */
descMatches(/^did/); /* Cannot match w. */
/* Equivalent to descMatch(/^.*did.*$/) . */
descMatches(/.*did.*/); /* Can match w. */
/* Equivalent to descMatch(/^l[ae]ng?$/) . */
descMatches(/l[ae]ng?/); /* Cannot match w. */
/* Equivalent to descMatch(/^.+$/) . */
descMatches(/.+/); /* Can match w. */
/* Equivalent to descMatch(/^(?:)$/) . */
descMatches(/(?:)/); /* Cannot match w. */
/* Equivalent to descMatch(/^spl\.?.+$/) . */
descMatches(new RegExp('spl\\.?.+$')); /* Cannot match w. */
```

### String Type

When the filter condition is a string type, it is equivalent to the `pattern` parameter of JavaScript's [RegExp.prototype.constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/RegExp) constructor, but it performs a full match from start to end, equivalent to automatically adding `^` at the start and `$` at the end.

For example, the string `'abc'` is treated as the regular expression `/^abc$/`,  
the string `'\\d+'` is treated as the regular expression `/^\d+$/`.

```js
w.desc(); // splendid
/* Equivalent to descMatch(/^s.*did$/) . */
descMatches('s.*did'); /* Cannot match w. */
/* Equivalent to descMatch(/^did$/) . */
descMatches('did'); /* Cannot match w. */
/* Equivalent to descMatch(/^did$/) . */
descMatches('did$'); /* Cannot match w. */
/* Equivalent to descMatch(/^did$/) . */
descMatches('^did'); /* Cannot match w. */
/* Equivalent to descMatch(/^.*did.*$/) . */
descMatches('.*did.*'); /* Can match w. */
/* Equivalent to descMatch(/^l[ae]ng?$/) . */
descMatches('l[ae]ng?'); /* Cannot match w. */
/* Equivalent to descMatch(/^.+$/) . */
descMatches('.+'); /* Can match w. */
/* Equivalent to descMatch(/^$/) . */
descMatches(''); /* Cannot match w. */
/* Equivalent to descMatch(/^spl\.?.+$/) . */
descMatches('spl\\.?.+$'); /* Cannot match w. */
```

For xxxMatches, matching patterns like the following are often seen:

```js
/* Equivalent to descMatch(/^.*word.*$/) . */
xxxMatches(/.*word.*/); /* or xxxMatches('.*word.*') . */
```

For xxxMatch, the matching style is often more in line with JavaScript developers' habits:

```js
xxxMatch(/word/);
```

The internal implementation of the xxxMatches method uses Java [matches](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#matches(java.lang.String)). The difference from JavaScript [match](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match) leads to the usage differences described above.

Therefore, in AutoJs6, all xxxMatches methods have been marked as `Deprecated`. Unless multi-version compatibility must be considered, it is always recommended to use xxxMatch instead of xxxMatches.

> See also: [Difference in results between Java matches vs JavaScript match](https://stackoverflow.com/questions/21883629/difference-in-results-between-java-matches-vs-javascript-match)

## xxxMatch

Regular expression matching filter.

The filter condition is of type [string](dataTypes#string) or [RegExp](dataTypes#regexp) and matches the control property string value according to regular expression rules.

### Regular Expression Type

When the filter condition is a regular expression type, the effect is equivalent to JavaScript's [RegExp.prototype.test](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test).

```js
w.desc(); // splendid
descMatch(/s.*did/); /* Can match w. */
descMatch(/did/); /* Can match w. */
descMatch(/did$/); /* Can match w. */
descMatch(/^did/); /* Cannot match w. */
descMatch(/l[ae]ng?/); /* Can match w. */
descMatch(/.+/); /* Can match w, same effect as descMatch(/(?:)/). */
descMatch(new RegExp('spl\\.?.+$')); /* Can match w. */
```

When the filter condition is a regular expression type, it supports [flags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#advanced_searching_with_flags) (also called `modifiers`):

```js
w.desc(); // AutoJs6
descMatch(/autojs6/i); /* Can match w. */
descMatch(new RegExp('autojs6', 'i')); /* Can match w. */
```

> Note: As of December 2022, the only supported flag is 'i'.

### String Type

When the filter condition is a string type, it is equivalent to the `pattern` parameter of JavaScript's [RegExp.prototype.constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/RegExp) constructor.

For example, the string `'abc'` is treated as the regular expression `/abc/`,  
the string `'\\d+'` is treated as the regular expression `/\d+/`.

```js
w.desc(); // splendid
/* Equivalent to descMatch(/s.*did/) . */
descMatch('s.*did'); /* Can match w. */
/* Equivalent to descMatch(/did/) . */
descMatch('did'); /* Can match w. */
/* Equivalent to descMatch(/did$/) . */
descMatch('did$'); /* Can match w. */
/* Equivalent to descMatch(/^did/) . */
descMatch('^did'); /* Cannot match w. */
/* Equivalent to descMatch(/l[ae]ng?/) . */
descMatch('l[ae]ng?'); /* Can match w. */
/* Equivalent to descMatch(/.+/) . */
descMatch('.+'); /* Can match w, same effect as descMatch(''). */
/* Equivalent to descMatch(/spl\.?.+$/) . */
descMatch('spl\\.?.+$'); /* Can match w. */
```

# Chaining Characteristics

Method chaining can be used to build multi-condition selectors:

```js
let sel = text("Start immediately").minHeight(0.2).clickable(true);
let w = sel.findOnce();
if (w !== null) { /* ... */ }
```

However, special attention is required: the `sel` variable in the example above is `mutable`:

```js
let sel = text("Start immediately").minHeight(0.2).clickable(true);

let wA = sel.findOnce();
if (wA != null) { /* ... */}
console.log(sel); // text("Start immediately").minHeight(0.2).clickable(true)

let wB = sel.descMatch(/\w+/).findOnce();
if (wB != null) { /* ... */}
console.log(sel); // text("Start immediately").minHeight(0.2).clickable(true).descMatch(/\w+/)

let wC = sel.findOnce();
if (wC != null) { /* ... */}
console.log(sel); // text("立即开始").minHeight(0.2).clickable(true).descMatch(/\w+/)
```

上述示例中, `wB` 变量赋值时, `sel.descMatch(/\w+/)` 使得 `sel` 发生改变.

此时的 `sel` 相当于是 `text("立即开始").minHeight(0.2).clickable(true).sel.descMatch(/\w+/)`.

因此 `wC` 与 `wA` 虽然使用了同样赋值语句, 但它们的 `sel` 并不相同.

将语句 `let wB = sel.descMatch(/\w+/).findOnce()`  
修改为 `let wB = sel.plus(descMatch(/\w+/)).findOnce()`  
即可保持 `sel` 变量不变.  

关于选择器的拼接, 可参阅 [plus](#m-plus) 与 [append](#m-append) 方法小节.