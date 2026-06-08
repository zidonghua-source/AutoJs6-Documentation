# Console

The AutoJs6 console is similar to the debugging console in web browsers. It is used for outputting information or assisting with code debugging.

## Showing the Console

AutoJs6 supports the following ways to display the console:

- Tap the "Log" icon in the top-right area of the AutoJs6 app home screen — opens the console Activity page.
- Use the code `console.launch()` — opens the console Activity page.
- Use the code `console.show()` — shows the console as a `Floating Window`.

## Module Purpose

The main purposes of the `console` module:

- Management of console log content — [display by log level / clear content / time tracking / stack traces / save to file], etc.
    - [console.log](#m-log)
    - [console.setGlobalLogConfig](#m-setgloballogconfig)
- Management of the console floating window — [window style / text style / show & hide / position & size], etc.
    - [console.show](#m-show)
- Management of the console Activity window
    - [console.launch](#m-launch)

Methods related to the console floating window only affect the floating window and have no effect on the Activity window:

```js
/* Change the font size of log text in the floating window to 23sp, */
/* but the log font in the Activity window is not affected. */

console.setContentTextSize(23);
console.show(); /* 浮动窗口日志字体 23sp. */

console.launch(); /* Activity 活动窗口的日志字体仍为默认大小. */
```

## 浮动窗口

使用 [console.show](#m-show) 可显示控制台的浮动窗口.

- 浮动窗口右上区域有三个操作按钮
    - 最小化按钮 - 收起浮动窗口并显示一个浮动按钮
    - 空间状态配置按钮 - 显示或隐藏空间状态 (位置及尺寸) 配置按钮
    - 关闭按钮 - 隐藏浮动窗口
- 拖动标题栏区域也可实现浮动窗口的位置移动
- 日志显示区域支持双指缩放改变文本字体大小

如需使用代码配置浮动窗口的外观与样式, 参阅 [console.build](#m-build) 小节.

一个简单的浮动窗口配置示例, 以便快速了解浮动窗口的配置方式:

- 尺寸 - 宽 80% 屏幕宽度, 高 60% 屏幕高度
- 位置 - X 坐标 10% 屏幕宽度, Y 坐标 15% 屏幕高度
- 标题 - HELLO WORLD
- 标题字号 - 18sp
- 标题背景颜色 - 900 号深橙色, 80% 透明度
- 日志字号 - 16sp
- 日志背景颜色 - 与标题背景颜色相同, 50% 透明度
- 浮动窗口在脚本结束后 6 秒钟自动隐藏

```js
/* 使用构建器方式. */

console.build({
    size: [ 0.8, 0.6 ],
    position: [ 0.1, 0.15 ],
    title: 'HELLO WORLD',
    titleTextSize: 18,
    contentTextSize: 16,
    backgroundColor: 'deep-orange-900',
    titleBackgroundAlpha: 0.8,
    contentBackgroundAlpha: 0.5,
    exitOnClose: 6e3,
}).show();

/* 使用链式配置方式. */

console
    .setSize(0.8, 0.6)
    .setPosition(0.1, 0.15)
    .setTitle('HELLO WORLD')
    .setTitleTextSize(18)
    .setContentTextSize(16)
    .setBackgroundColor('deep-orange-900')
    .setTitleBackgroundAlpha(0.8)
    .setContentBackgroundAlpha(0.5)
    .setExitOnClose(6e3)
    .show();

/* 使用传统分步配置方式. */

console.setSize(0.8, 0.6);
console.setPosition(0.1, 0.15);
console.setTitle('HELLO WORLD');
console.setTitleTextSize(18);
console.setContentTextSize(16);
console.setBackgroundColor('deep-orange-900');
console.setTitleBackgroundAlpha(0.8);
console.setContentBackgroundAlpha(0.5);
console.setExitOnClose(6e3);
console.show();
```

---

<p style="font: bold 2em sans-serif; color: #FF7043">console</p>

---

## [m] show

### show()

**`[6.3.0]`**

- <ins>**returns**</ins> { [this](console) }

Displays the console floating window.

The floating window's style and spatial state can be configured either before or after it is shown.  
For example, to set the window size to `500` × `800`:

```js
/* Set size before show. */

console.setSize(500, 800);
console.show();

/* Set size after show. */

console.show();
console.setSize(500, 800);

/* Both examples above support method chaining. */
console.show().setSize(500, 800);
console.setSize(500, 800).show();
```

## [m] isShowing

### isShowing()

**`6.3.0`**

- <ins>**returns**</ins> { [boolean](dataTypes#boolean) }

Returns whether the console floating window is not in a hidden state.

Non-hidden states include:

- The floating window is expanded and visible
- The floating window is collapsed (minimized)

```js
console.show();
console.isShowing(); // true

console.collapse(); /* Collapse (minimize) the floating window. */
console.isShowing(); /* Still returns true. */

console.hide(); /* Hide the floating window. */
console.isShowing(); // false
```

## [m] hide

### hide()

**`[6.3.0]`**

- <ins>**returns**</ins> { [this](console) }

Hides the console floating window.

After hiding, the style and spatial state are preserved, even after the script ends:

```js
console.show();
console.setSize(500, 800);
console.hide();
```

If you then run the following code in another script:

```js
console.show();
```

The floating window will still appear with the size `500` × `800` — the previous configuration is restored.

To restore default window configuration before showing, use `console.reset()`:

```js
console.reset();
console.show();
```

## [m] reset

### reset()

**`6.3.0`**

- <ins>**returns**</ins> { [this](console) }

Resets the style and spatial state of the console floating window to its default values.

The `reset` method can also be used while the floating window is visible:

```js
console.setSize(500, 800).show();
setTimeout(console.reset, 2e3); /* Reset after 2 seconds. */
```

## [m] collapse

### collapse()

**`6.3.0`**

- <ins>**returns**</ins> { [this](console) }

Collapses (minimizes) the console floating window.

## [m] expand

### expand()

**`6.3.0`**

- <ins>**returns**</ins> { [this](console) }

Expands the console floating window.

When using [console.show](#m-show) to display the window, it is expanded by default.

## [m] launch

### launch()

**`6.3.0`**

- <ins>**returns**</ins> { [void](dataTypes#void) }

Launches the console Activity window.

This method is equivalent to tapping the "Log" icon in the top-right area of the AutoJs6 home screen.

## [m] build

### build(options)

**`6.3.0`**

- **options** { [ConsoleBuildOptions](consoleBuildOptionsType) } - Builder options
- <ins>**returns**</ins> {{ show(): [void](dataTypes#void) }}

Builds the configuration for the console floating window.

After building, call the `show` method to display the floating window: `console.build({ ... }).show()`.

The builder supports configuring multiple floating window style options at once:

```js
console.build({
    size: [ 0.8, 0.6 ], /* Window size: 80% screen width × 60% screen height. */
    position: [ 0.1, 0.15 ], /* Window position: X = 10% screen width, Y = 15% screen height. */
    title: 'HELLO WORLD', /* Window title text. */
    titleTextSize: 18, /* Title font size in sp. */
    contentTextSize: 16, /* Log font size in sp. */
    backgroundColor: 'deep-orange-900', /* Background color for title and log areas (deep orange 900). */
    titleBackgroundAlpha: 0.8, /* Title area background opacity: 80%. */
    contentBackgroundAlpha: 0.5, /* Log area background opacity: 50%. */
    exitOnClose: 6e3, /* Automatically close the window 6 seconds after the script ends. */
    touchable: true, /* true: window responds to taps normally; false: taps pass through the window. */
}).show(); /* Use the show method to display the floating window. */
```

For more builder parameters and usage, see the [ConsoleBuildOptions](consoleBuildOptionsType) type chapter.

## [m] setSize

### setSize(width, height)

**`[6.3.0]`**

- **width** { [number](dataTypes#number) } - Floating window width (pixels or percentage)
- **height** { [number](dataTypes#number) } - Floating window height (pixels or percentage)
- <ins>**returns**</ins> { [this](console) }

Sets the size of the console floating window.

```js
console.setSize(0.8, 700).show(); /* 80% screen width, 700 pixels height. */
console.build({ size: [ 0.8, 700 ] }).show(); /* Same effect. */
```

## [m] setPosition

### setPosition(x, y)

**`[6.3.0]`**

- **x** { [number](dataTypes#number) } - Floating window X coordinate (pixels or percentage)
- **y** { [number](dataTypes#number) } - Floating window Y coordinate (pixels or percentage)
- <ins>**returns**</ins> { [this](console) }

Sets the position of the console floating window.

```js
console.setPosition(0.1, 0.15).show(); /* X: 10% screen width, Y: 15% screen height. */
console.build({ position: [ 0.1, 0.15 ] }).show(); /* Same effect. */
```

## [m] setExitOnClose

### setExitOnClose(exitOnClose?)

**`6.3.0`** **`Overload 1/2`**

- [ `true` ] **exitOnClose** { [boolean](dataTypes#boolean) } - Whether the floating window closes automatically
- <ins>**returns**</ins> { [this](console) }

Sets whether the console floating window should automatically close when the script ends.

```js
console.setExitOnClose(true).show(); /* Auto-close enabled: floating window closes 5 seconds after script ends. */
console.setExitOnClose().show(); /* Parameter omitted, same effect. */
console.build({ exitOnClose: true }).show(); /* Same effect. */

console.setExitOnClose(false).show(); /* Disable auto-close. */
console.build({ exitOnClose: false }).show(); /* Same effect. */
```

### setExitOnClose(timeout)

**`6.3.0`** **`Overload 2/2`**

- **timeout** { [number](dataTypes#number) } - Timeout (in milliseconds) before the floating window auto-closes
- <ins>**returns**</ins> { [this](console) }

Sets the timeout (in milliseconds) after which the console floating window will automatically close when the script ends.

```js
console.setExitOnClose(6e3).show(); /* Floating window auto-closes 6 seconds after script ends. */
console.build({ exitOnClose: 6e3 }).show(); /* Same effect. */
```

## [m] setTouchable

### setTouchable(touchable?)

**`6.5.0`**

- [ `true` ] **touchable** { [boolean](dataTypes#boolean) } - Whether to respond to tap events
- <ins>**returns**</ins> { [this](console) }

Sets whether the console floating window responds to tap events. Default is `true`.

Set to `false` to make taps pass through the window.

```js
console.setTouchable(false).show(); /* Tap events will pass through the console floating window. */
console.build({ touchable: false }).show(); /* Same effect. */
```

When `setTouchable` is set to `false`, the close button at the top of the floating window cannot be triggered by tapping. You can close the window programmatically using [hide](#m-hide) or [setExitOnClose](#m-setexitonclose):

```js
/* Use setExitOnClose to auto-close the window after the script ends. */

console
    .setTouchable(false)
    .setExitOnClose(true)
    .show();

/* Builder syntax. */

console.build({
    touchable: false,
    exitOnClose: true,
}).show();

/* Use volume keys to close (requires Accessibility service). */

events.observeKey();
events.setKeyInterceptionEnabled(true);
events.on('volume_down', () => {
    console.hide();
    exit(); /* Optional: exit the script. */
});
```

## [m] setTitle

### setTitle(title)

**`[6.3.0]`**

- **title** { [string](dataTypes#string) } - Floating window title text
- <ins>**returns**</ins> { [this](console) }

Sets the title text of the console floating window.

```js
console.setTitle('Air Conditioner Temperature Monitor').show();
console.build({ title: 'Air Conditioner Temperature Monitor' }).show(); /* Same effect. */
```

## [m] setTitleTextSize

### setTitleTextSize(size)

**`6.3.0`**

- **size** { [number](dataTypes#number) } - Floating window title font size
- <ins>**returns**</ins> { [this](console) }

Sets the font size of the console floating window title (in `sp`).

```js
console.setTitleTextSize(20).show(); /* Set title font size to 20sp. */
console.build({ titleTextSize: 20 }).show(); /* Same effect. */
```

## [m] setTitleTextColor

### setTitleTextColor(color)

**`6.3.0`**

- **color** { [OmniColor](omniTypes#omnicolor) } - Floating window title text color
- <ins>**returns**</ins> { [this](console) }

Sets the text color of the console floating window title.

```js
console.setTitleTextColor('dark-orange').show(); /* Set title color to dark orange. */
console.build({ titleTextColor: 'dark-orange' }).show(); /* Same effect. */
```

## [m] setTitleBackgroundColor

### setTitleBackgroundColor(color)

**`6.3.0`**

- **color** { [OmniColor](omniTypes#omnicolor) } - Background color of the floating window title area
- <ins>**returns**</ins> { [this](console) }

Sets the background color of the console floating window's title area.

```js
/* Set title area background to dark blue. */
console.setTitleBackgroundColor('dark-blue').show();
console.build({ titleBackgroundColor: 'dark-blue' }).show(); /* Same effect. */

/* Set title area background to semi-transparent dark blue. */
console.setTitleBackgroundColor(Color('dark-blue').setAlpha(0.5)).show();
console.setTitleBackgroundColor('#8000008B').show(); /* Same effect. */

/* Opacity can also be set separately using setTitleBackgroundAlpha. */
console
    .setTitleBackgroundColor('dark-blue')
    .setTitleBackgroundAlpha(0.5)
    .show();
```

## [m] setTitleBackgroundAlpha

### setTitleBackgroundAlpha(alpha)

**`6.3.0`**

- **alpha** { [number](dataTypes#number) } - Background opacity of the floating window title area
- <ins>**returns**</ins> { [this](console) }

Sets the background opacity of the console floating window's title area.

```js
/* Set title area background to semi-transparent. */
console.setTitleBackgroundAlpha(0.5).show();
console.build({ titleBackgroundAlpha: 0.5 }).show(); /* Same effect. */

/* Set title area background to semi-transparent dark blue. */
console
    .setTitleBackgroundColor('dark-blue')
    .setTitleBackgroundAlpha(0.5)
    .show();
```

## [m] setTitleIconsTint

### setTitleIconsTint(color)

**`6.3.0`**

- **color** { [OmniColor](omniTypes#omnicolor) } - Tint color for floating window action buttons
- <ins>**returns**</ins> { [this](console) }

Sets the tint color for the console floating window's action buttons.

```js
/* Set action button tint to green. */
console.setTitleIconsTint('green').show();
console.build({ titleIconsTint: 'green' }).show(); /* Same effect. */
```

## [m] setContentTextSize

### setContentTextSize(size: number)

**`6.3.0`**

- **param** { [number](dataTypes#number) } - Floating window log text font size
- <ins>**returns**</ins> { [this](console) }

Sets the font size of the console floating window log text (in `sp`).

```js
/* Set log text font size to 18sp. */
console.setContentTextSize(18).show();
console.build({ contentTextSize: 18 }).show(); /* Same effect. */
```

## [m] setContentTextColor

### setContentTextColor(colorMap)

**`6.3.0`** **`Overload 1/2`**

- **colorMap** {{
    - verbose?: [OmniColor](omniTypes#omnicolor);
    - log?: [OmniColor](omniTypes#omnicolor);
    - info?: [OmniColor](omniTypes#omnicolor);
    - warn?: [OmniColor](omniTypes#omnicolor);
    - error?: [OmniColor](omniTypes#omnicolor);
    - assert?: [OmniColor](omniTypes#omnicolor);
- }} - Log text color map for the floating window

Sets the log text colors of the console floating window. You can specify different colors for different log levels.

```js
/* Set LOG level log text color to dark orange. */
console.setContentTextColor({ log: 'dark-orange' }).show();
console.log('content text color test for console.log');

/* Set ERROR level log text color to dark red. */
console.setContentTextColor({ error: 'dark-red' }).show();
console.error('content text color test for console.error');

/* Set colors for multiple log levels. */
console.setContentTextColor({
    verbose: 'gray',
    log: 'white',
    info: 'light-green',
    warn: 'light-blue',
    error: 'red',
}).show();
[ 'verbose', 'log', 'info', 'warn', 'error' ].forEach((fName) => {
    console[fName].call(console, `content text color test for console.${fName}`);
});
```

### setContentTextColor(color)

**`6.3.0`** **`Overload 2/2`**

- **colors** { [OmniColor](omniTypes#omnicolor) } - Unified text color for all logs in the floating window
- <ins>**returns**</ins> { [this](console) }

Sets a single unified text color for all log messages in the console floating window (does not distinguish between log levels).

```js
/* Set all log text color to dark green. */
console.setContentTextColor('dark-green').show();
[ 'verbose', 'log', 'info', 'warn', 'error' ].forEach((fName) => {
    console[fName].call(console, `content text color test for console.${fName}`);
});
```

## [m] setContentBackgroundColor

### setContentBackgroundColor(color)

**`6.3.0`**

- **color** { [OmniColor](omniTypes#omnicolor) } - Background color of the floating window log display area
- <ins>**returns**</ins> { [this](console) }

Sets the background color of the console floating window's log display area.

```js
/* Set log display area background to dark blue. */
console.setContentBackgroundColor('dark-blue').show();
console.build({ contentBackgroundColor: 'dark-blue' }).show(); /* Same effect. */

/* Set log display area background to semi-transparent dark blue. */
console.setContentBackgroundColor(Color('dark-blue').setAlpha(0.5)).show();
console.setContentBackgroundColor('#8000008B').show(); /* Same effect. */

/* Opacity can also be set separately using setContentBackgroundAlpha. */
console
    .setContentBackgroundColor('dark-blue')
    .setContentBackgroundAlpha(0.5)
    .show();
```

## [m] setContentBackgroundAlpha

### setContentBackgroundAlpha(alpha)

**`6.3.0`**

- **alpha** { [number](dataTypes#number) } - Background opacity of the floating window log display area
- <ins>**returns**</ins> { [this](console) }

Sets the background opacity of the console floating window's log display area.

```js
/* Set log display area background to semi-transparent. */
console.setContentBackgroundAlpha(0.5).show();
console.build({ contentBackgroundAlpha: 0.5 }).show(); /* Same effect. */

/* Set log display area background to semi-transparent dark blue. */
console
    .setContentBackgroundColor('dark-blue')
    .setContentBackgroundAlpha(0.5)
    .show();
```

## [m] setTextSize

### setTextSize(size)

**`6.3.0`**

- **size** { [number](dataTypes#number) } - Font size for both title and log text in the floating window
- <ins>**returns**</ins> { [this](console) }

Sets the font size (in `sp`) for both the title and log text of the console floating window.

This is a convenience method that combines [setTitleTextSize](#m-settitletextsize) and [setContentTextSize](#m-setcontenttextsize).

```js
/* Set both title and log text size to 18sp. */
console.setTextSize(18).show();
console.build({ textSize: 18 }).show(); /* Same effect. */
```

## [m] setTextColor

### setTextColor(color)

**`6.3.0`**

- **color** [OmniColor](omniTypes#omnicolor) } - Text color for title and log text in the floating window
- <ins>**returns**</ins> { [this](console) }

Sets the text color for both the title and log text of the console floating window.

For log text, a single color is applied to all levels (no distinction between log levels).

This is a convenience method that combines [setTitleTextColor](#m-settitletextcolor) and [setContentTextColor](#m-setcontenttextcolor).

```js
/* Set all title and log text color to light blue. */
console.setTextColor('light-blue').show();
[ 'verbose', 'log', 'info', 'warn', 'error' ].forEach((fName) => {
    console[fName].call(console, ` text color test for console.${fName}`);
});
```

## [m] setBackgroundColor

### setBackgroundColor(color)

**`6.3.0`**

- **color** { [OmniColor](omniTypes#omnicolor) } - Background color for title and log display areas
- <ins>**returns**</ins> { [this](console) }

Sets the background color for both the title and log display areas of the console floating window.

This is a convenience method that combines [setTitleBackgroundColor](#m-settitlebackgroundcolor) and [setContentBackgroundColor](#m-setcontentbackgroundcolor).

```js
/* Set title and log display area background to light yellow. */
console.setBackgroundColor('light-yellow').show();
console.build({ backgroundColor: 'light-yellow' }).show(); /* Same effect. */

/* Set title and log display area background to semi-transparent light yellow. */
console.setBackgroundColor(Color('light-yellow').setAlpha(0.5)).show();
console.setBackgroundColor('#80FFFFE0').show(); /* Same effect. */

/* Opacity can also be set separately using backgroundAlpha. */
console
    .setBackgroundColor('light-yellow')
    .setBackgroundAlpha(0.5)
    .show();
```

## [m] setBackgroundAlpha

### setBackgroundAlpha(alpha)

**`6.3.0`**

- **alpha** { [number](dataTypes#number) } - Background opacity for title and log display areas
- <ins>**returns**</ins> { [this](console) }

Sets the background opacity for both the title and log display areas of the console floating window.

This is a convenience method that combines [setTitleBackgroundAlpha](#m-settitlebackgroundalpha) and [setContentBackgroundAlpha](#m-setcontentbackgroundalpha).

```js
/* Set title and log display area background to semi-transparent. */
console.setBackgroundAlpha(0.5).show();
console.build({ backgroundAlpha: 0.5 }).show(); /* Same effect. */

/* Set title and log display area background to semi-transparent light yellow. */
console
    .setBackgroundColor('light-yellow')
    .setBackgroundAlpha(0.5)
    .show();
```

## [m] verbose

### verbose(data, ...args)

**`Global`**

- **data** { [string](dataTypes#string) } - Object to format (may contain placeholders)
- **args** { [...](documentation#可变参数)[any](dataTypes#any)[[]](documentation#可变参数) } - [Placeholder replacement arguments](glossaries#占位符替换参数)
- <ins>**returns**</ins> { [void](dataTypes#void) }

Outputs the arguments to the console.

Main uses: test messages / debug messages / lowest importance messages

Priority: **verbose** < log < info < warn < error < assert

Text colors:

- Floating window — [ <span style="color: #E0E0E0">◑</span> ] — #E0E0E0
- Activity window
    - Light theme — [ <span style="color: #C0C0C0">◑</span> ] — #DFC0C0C0
    - Dark theme — [ <span style="color: #7F7F80">◑</span> ] — #7F7F80

> Note: This method automatically appends a newline at the end.

## [m] log

### log(data, ...args)

**`Global`**

- **data** { [string](dataTypes#string) } - Object to format (may contain placeholders)
- **args** { [...](documentation#可变参数)[any](dataTypes#any)[[]](documentation#可变参数) } - [Placeholder replacement arguments](glossaries#占位符替换参数)
- <ins>**returns**</ins> { [void](dataTypes#void) }

Outputs the arguments to the console.

Main uses: normal messages

Priority: verbose < **log** < info < warn < error < assert

Text colors:

- Floating window — [ <span style="color: #FFFFFF">◑</span> ] — #FFFFFF
- Activity window
    - Light theme — [ <span style="color: #000000">◑</span> ] — #CC000000
    - Dark theme — [ <span style="color: #E0E0E0">◑</span> ] — #DFE0E0E0

> Note: This method automatically appends a newline at the end.

## [m] info

### info(data, ...args)

- **data** { [string](dataTypes#string) } - Object to format (may contain placeholders)
- **args** { [...](documentation#可变参数)[any](dataTypes#any)[[]](documentation#可变参数) } - [Placeholder replacement arguments](glossaries#占位符替换参数)
- <ins>**returns**</ins> { [void](dataTypes#void) }

Outputs the arguments to the console.

Main uses: important messages / noteworthy messages

Priority: verbose < log < **info** < warn < error < assert

Text colors:

- Floating window — [ <span style="color: #DCEDC8">◑</span> ] — #DCEDC8
- Activity window — [ <span style="color: #43A047">◑</span> ] — #43A047

> Note: This method automatically appends a newline at the end.

## [m] warn

### warn(data, ...args)

**`Global`**

- **data** { [string](dataTypes#string) } - Object to format (may contain placeholders)
- **args** { [...](documentation#可变参数)[any](dataTypes#any)[[]](documentation#可变参数) } - [Placeholder replacement arguments](glossaries#占位符替换参数)
- <ins>**returns**</ins> { [void](dataTypes#void) }

Outputs the arguments to the console.

Main uses: warning messages / potential issue messages

Priority: verbose < log < info < **warn** < error < assert

Text colors:

- Floating window — [ <span style="color: #B3E5FC">◑</span> ] — #B3E5FC
- Activity window — [ <span style="color: #1976D2">◑</span> ] — #1976D2

> Note: This method automatically appends a newline at the end.

## [m] error

### error(data, ...args)

- **data** { [string](dataTypes#string) } - Object to format (may contain placeholders)
- **args** { [...](documentation#可变参数)[any](dataTypes#any)[[]](documentation#可变参数) } - [Placeholder replacement arguments](glossaries#占位符替换参数)
- <ins>**returns**</ins> { [void](dataTypes#void) }

Outputs the arguments to the console.

Main uses: error messages / exception messages

Priority: verbose < log < info < warn < **error** < assert

Text colors:

- Floating window — [ <span style="color: #FFCDD2">◑</span> ] — #FFCDD2
- Activity window — [ <span style="color: #C62828">◑</span> ] — #C62828

> Note: This method automatically appends a newline at the end.

## [m] assert

### assert(bool, message?)

**`6.3.0`** **`Overload [1-2]/4`**

- **bool** { [boolean](dataTypes#boolean) } - Assertion value
- **[ message ]** { [string](dataTypes#string) } - Message to display if assertion fails
- <ins>**returns**</ins> { [void](dataTypes#void) }

Asserts that the `bool` parameter is true.

If the assertion fails, the script stops and outputs the failure message along with the call stack to the console.

Main uses: asserting a variable

Priority: verbose < log < info < warn < error < **assert**

Text colors:

- Floating window — [ <span style="color: #FCE4EC">◑</span> ] — #FCE4EC
- Activity window — [ <span style="color: #E254FF">◑</span> ] — #E254FF

```js
console.assert(new Date().getSeconds() < 30, 'Assertion failed: current time in seconds is not less than 30');
```

> Note: This method automatically appends a newline at the end of the console message.

### assert(func, message?)

**`6.3.0`** **`Overload [3-4]/4`**

- **func** { [() =>](#function) [boolean](dataTypes#boolean) } - Assertion value
- **[ message ]** { [string](dataTypes#string) } - Message to display if assertion fails
- <ins>**returns**</ins> { [void](dataTypes#void) }

Asserts that the result of executing `func` is true.

If the assertion fails, the script stops and outputs the failure message along with the call stack to the console.

Main uses: asserting a function

Priority: verbose < log < info < warn < error < **assert**

Text colors:

- Floating window — [ <span style="color: #FCE4EC">◑</span> ] — #FCE4EC
- Activity window — [ <span style="color: #E254FF">◑</span> ] — #E254FF

```js
console.assert(function () {
    return new Date().getSeconds() < 30;
}, 'Assertion failed: current time in seconds is not less than 30');
```

> Note: This method automatically appends a newline at the end of the console message.

## [m] clear

### clear()

**`6.3.0`**

- <ins>**returns**</ins> { [this](console) }

Clears all log content from the console.

## [m] print

### print(data, ...args)

**`Global`** **`DEPRECATED`**

- **data** { [string](dataTypes#string) } - Object to format (may contain placeholders)
- **args** { [...](documentation#可变参数)[any](dataTypes#any)[[]](documentation#可变参数) } - [Placeholder replacement arguments](glossaries#占位符替换参数)
- <ins>**returns**</ins> { [void](dataTypes#void) }

Equivalent to [console.log](#m-log).

> Note: In AutoJs6, the `print` method behaves more like `println` in other languages. Additionally, in browsers the global `print` method is used to print the current page. For these reasons, the global `print` method has been deprecated and is not recommended.

## [m] printAllStackTrace

### printAllStackTrace(e)

**`6.3.0`**

- **e** { [OmniThrowable](omniTypes#omnithrowable) } - Exception object
- <ins>**returns**</ins> { [void](dataTypes#void) }

Prints detailed stack trace information to the console.

```js
try {
    null.toString()
} catch (e) {
    /* Print a simple error message. */
    /* Usually only 1 line. */
    console.error(e.message);

    /* Use the exit method to throw an exception. */
    /* Usually fewer than 10 lines. */
    exit(e);

    /* Use console.printAllStackTrace to print the full stack trace. */
    /* Usually dozens of lines. */
    console.printAllStackTrace(e);
}
```

## [m] trace

### trace(message, level?)

**`6.3.0`**

- **message** { [string](dataTypes#string) } - Trace message
- **[ level = "debug" ]** { `'verbose'` | `'debug'` | `'info'` | `'warn'` | `'error'` | [number](dataTypes#number) } - Output log level
- <ins>**returns**</ins> { [void](dataTypes#void) }

Outputs the current call stack trace information to the console.

The `level` parameter accepts string shortcuts derived from integer constants:

| String      | Integer Constant                                        | Description                                                                 |
|-------------|---------------------------------------------------------|-----------------------------------------------------------------------------|
| 'verbose'   | <span style="white-space:nowrap">Log.VERBOSE = 2</span> | <span style="white-space:nowrap">Corresponds to [console.verbose](#m-verbose) level.</span> |
| **'debug'** | <span style="white-space:nowrap">Log.DEBUG = 3</span>   | <span style="white-space:nowrap">Corresponds to [console.log](#m-log) level.</span>         |
| 'info'      | <span style="white-space:nowrap">Log.INFO = 4</span>    | <span style="white-space:nowrap">Corresponds to [console.info](#m-info) level.</span>       |
| 'warn'      | <span style="white-space:nowrap">Log.WARN = 5</span>    | <span style="white-space:nowrap">Corresponds to [console.warn](#m-warn) level.</span>       |
| 'error'     | <span style="white-space:nowrap">Log.ERROR = 6</span>   | <span style="white-space:nowrap">Corresponds to [console.error](#m-error) level.</span>     |

```js
function printMessages() {
    console.trace('This is a "normal" message for test');
    console.trace('This is an "info" message for test', 'info');
    console.trace('This is a "warn" message for test', 'warn');
    console.trace('This is an "error" message for test', 'error');
    console.launch();
}

({
    init() {
        this.intermediate();
    },
    intermediate() {
        printMessages();
    },
}).init();

// Example of ERROR level trace output:
// 20:46:00.709/E: This is an "error" message for test
// 	at consoleTrace.js:5 (printMessages)
// 	at consoleTrace.js:14
// 	at consoleTrace.js:11
// 	at consoleTrace.js:9
```

## [m] time

### time(label?)

- **[ label ]** { [string](dataTypes#string) } - 计时标签
- <ins>**returns**</ins> { [void](dataTypes#void) }

启动计时器, 用以计算以 `label` 参数标记的时间间隔.

[console.timeEnd](#m-timeend) 传入与 `label` 参数相同的值时, 计时器停止, 并输出时间间隔信息到控制台.

多次使用 time 方法传入相同 `label` 时, 将重置其关联的计时器.

```js
console.time('fruit');
sleep(2e3);
console.timeEnd('fruit');
```

## [m] timeEnd

### timeEnd(label?)

- **[ label ]** { [string](dataTypes#string) } - 计时标签
- <ins>**returns**</ins> { [void](dataTypes#void) }

与 console.time 配合使用, 用以计算以 `label` 参数标记的时间间隔.

`label` 关联的计时器不存在时, 打印 `NaNms`.

```js
console.time('fruit');
sleep(2e3);
console.timeEnd('fruit');
```

## [m] setGlobalLogConfig

### setGlobalLogConfig(config)

- **config** {{
    - [ file = `'android-log4j.log'` ]?: [string](dataTypes#string) - 待写入日志的文件路径, 支持绝对路径及相对路径
    - [ maxFileSize = `512 * 1024` ]?: [number](dataTypes#number) - 文件的分卷阈值容量 (单位为字节)
    - [ maxBackupSize = `5` ]?: [number](dataTypes#number) - 文件最大备份数量, 达到上限后将替换最旧文件
    - [ rootLevel = `'all'` ]?: `'all'` | `'off'` | `'debug'` | `'info'` | `'warn'` | `'error'` | `'fatal'` - 日志写入级别
    - [ filePattern = `'%d - [%p::%c::%C] - %m%n'` ]?: [string](dataTypes#string) - 日志写入格式, 参阅 [PatternLayout](https://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/PatternLayout.html)
- }} - 日志输出至文件的配置选项
- <ins>**returns**</ins> { [void](dataTypes#void) }

设置将全局日志写入文件的配置选项.

该方法会影响所有脚本的日志记录.

```js
console.setGlobalLogConfig({
    file: `./log/${Date.now()}.log`,
    filePattern: '%d{yyyy-MM-dd/}%m%n',
    maxBackupSize: 16,
    maxFileSize: 384 << 10, /* 384 KB. */
});
```

## [m] resetGlobalLogConfig

### resetGlobalLogConfig()

**`6.3.1`**

- <ins>**returns**</ins> { [void](dataTypes#void) }

重置全局日志写入配置.

此方法可重置 [setGlobalLogConfig](#m-setgloballogconfig) 的全部选项配置.

## [m] input

### input(data, ...args)

**`ABANDONED`**

- **data** { [string](dataTypes#string) } - 可包含占位符的待格式化对象
- **args** { [...](documentation#可变参数)[any](dataTypes#any)[[]](documentation#可变参数) } - [占位符替换参数](glossaries#占位符替换参数)
- <ins>**returns**</ins> { [void](dataTypes#void) }

此方法已于 `6.3.1` 版本被废弃, 使用后将无任何效果.

## [m] rawInput

### rawInput(data, ...args)

**`ABANDONED`**

- **data** { [string](dataTypes#string) } - 可包含占位符的待格式化对象
- **args** { [...](documentation#可变参数)[any](dataTypes#any)[[]](documentation#可变参数) } - [占位符替换参数](glossaries#占位符替换参数)
- <ins>**returns**</ins> { [void](dataTypes#void) }

此方法已于 `6.3.1` 版本被废弃, 使用后将无任何效果.