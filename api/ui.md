# User Interface (UI)

---

<p style="font: italic 1em sans-serif; color: #78909C">This chapter is pending supplementation or improvement...</p>
<p style="font: italic 1em sans-serif; color: #78909C">Marked by SuperMonster003 on Oct 22, 2022.</p>

---

The `ui` module provides support for writing user interfaces.

    Reminder for Android developers or advanced users: Auto.js's UI system originates from Android. All properties and methods can be found in the Android source code. If certain code or properties do not appear in the Auto.js documentation, you may refer to the Android documentation.
    View: https://developer.android.google.cn/reference/android/view/View?hl=cn
    Widget: https://developer.android.google.cn/reference/android/widget/package-summary?hl=cn

Scripts that use UI must start with `"ui";` to specify UI mode; otherwise, the script will not run in UI mode. Correct example:

```
"ui";

// Other script code
```

Comments, blank lines, and spaces may appear before the string `"ui"` **[added in v4.1.0]**, but no other code is allowed.

An interface is composed of Views. Views are divided into two types: Widgets (controls) and Layouts. Widgets are used to display text, images, web pages, etc. For example, the text widget (`text`) displays text, the button widget (`button`) displays a button and provides click effects, the image widget (`img`) displays images from the network or files, and there are also input widgets (`input`), progress bar widgets (`progressbar`), checkbox widgets (`checkbox`), etc. Layouts are "containers" that hold one or more widgets and are used to control the position of the widgets inside them. For example, a vertical layout (`vertical`) displays its widgets from top to bottom (i.e., vertically arranged), a horizontal layout (`horizontal`) displays its widgets from left to right (i.e., horizontally arranged), and a frame layout (`frame`) displays its widgets directly in the upper-left corner. If there are multiple widgets, later widgets will overlap earlier ones.

We use XML to write interfaces and specify the layout XML of the interface through the `ui.layout()` function. For example:

```
"ui";
$ui.layout(
    <vertical>
        <button text="First button"/>
        <button text="Second button"/>
    </vertical>
);
```

In this example, lines 3~6 are the XML that specifies the specific content of the interface. The `<vertical> ... </vertical>` tag on line 3 represents a vertical layout. Layout tags usually start with `<...>` and end with `</...>`. The content between the two tags is the content inside the layout, for example `<frame> ... </frame>`. In this example, the content on lines 4 and 5 is the content inside the vertical layout. Line 4 is a button widget (`button`). Widget tags usually start with `<...` and end with `/>`. Between them are the specific properties of the widget, for example `<text ... />`. In this example, `text="First button"` is a property of the button widget that specifies the text content of this button.

Line 5 is the same as line 4 — also a button widget — except its text content is "Second button". These two widgets are inside the vertical layout, so they will be arranged vertically. The effect is shown below:

![ex1](images/ex1.png)

If we change the vertical layout (`vertical`) in this example to a horizontal layout (`horizontal`), that is:

```
"ui";
ui.layout(
    <horizontal>
        <button text="First button"/>
        <button text="Second button"/>
    </horizontal>
);
```

Then the two buttons will be arranged horizontally. The effect is shown below:

![ex1-horizontal](images/ex1-horizontal.png)

A widget can specify multiple properties (or even none at all), separated by spaces. Layouts can also specify properties. For example:

```
"ui";
ui.layout(
    <vertical bg="#ff0000">
        <button text="First button" textSize="20sp"/>
        <button text="Second button"/>
    </vertical>
);
```

The third line `bg="#ff0000"` specifies that the background color (`bg`) of the vertical layout is "#ff0000", which is an RGB color representing red (for RGB-related knowledge, see the [RGB Color Reference Table](http://tool.oschina.net/commons?type=3)). The fourth line `textSize="20sp"` specifies that the font size (`textSize`) of the button widget is "20sp". "sp" is a font unit; there is no need to go deep into it for now. The effect of the above code is shown below:

![ex-properties](images/ex1-properties.png)

An interface consists of some layouts and widgets. For easier document reading, we will explain the following terms:

* Child view, child widget: The widgets inside a layout are the child widgets/child views of that layout. In fact, a layout can contain not only widgets but also nested layouts. Therefore, "child view (Child View)" is more accurate. In the example above, the buttons are child widgets of the vertical layout.
* Parent view, parent layout: The layout that directly contains a widget is the parent layout / parent view (Parent View) of that widget. In the example above, the vertical layout is the parent layout of the buttons.

# Views: View

Both widgets and layouts belong to Views. This chapter introduces the common properties and functions shared by all widgets and layouts. For example, the background property, width and height (all widgets and layouts can set background and width/height), and the `click()` function to set the action to execute when the View is clicked.

## attr(name, value)

* `name` {string} Property name
* `value` {string} Property value

Set the value of a property. The property name refers to the attribute in the View's XML. For example, you can set the text value of a text widget using `attr("text", "text")`.

```javascript
"ui";

$ui.layout(
    <frame>
        <text id="example" text="Hello"/>
    </frame>
);

// Execute after 5 seconds
$ui.post(() => {
    // Modify text
    $ui.example.attr("text", "Hello, Auto.js UI");
    // Modify background
    $ui.example.attr("bg", "#ff00ff");
    // Modify height
    $ui.example.attr("h", "500dp");
}, 5000);
```

**Note:** Not all properties can be set in JS code. Some properties can only be set when the layout is created, such as the `style` property. Some properties can be set in code but are not yet supported. In these cases, Auto.js Pro 8.1.0+ will throw an exception, while other versions will not.

## attr(name)

* `name` {string} Property name
* Returns {string}

Get the value of a property.

```javascript
"ui";

$ui.layout(
    <frame>
        <text id="example" text="1"/>
    </frame>
);

plusOne();

function plusOne() {
    // Get text
    let text = $ui.example.attr("text");
    // Parse as number
    let num = parseInt(text);
    // Add 1 to the number
    num++;
    // Set text
    $ui.example.attr("text", String(num));
    // Continue after 1 second
    $ui.post(plusOne, 1000);
}

```

## w

The width of the View, shorthand for the `width` property. Possible values are `*`, `auto`, and specific numbers. `*` means the width will **try its best** to fill the parent layout, while `auto` means the width will automatically adjust based on the View's content (adaptive width). For example:

```
"ui";
ui.layout(
    <horizontal>
        <button w="auto" text="Adaptive width"/>
        <button w="*" text="Fill parent layout"/>
    </horizontal>
);
```

In this example, the first button has adaptive width, and the second button fills the parent layout. The display effect is:

![ex-w](images/ex-w.png)

If this property is not set, different widgets and layouts have different default widths, most of which are `auto`.

The width property can also specify a specific value, such as `w="20"`, `w="20px"`, etc. Without a unit, the default unit is dp. Other units include px (pixels), mm (millimeters), and in (inches). For more information about dimension units, see [Dimension Units: Dimension](#ui_尺寸的单位_Dimension).

```
"ui";
ui.layout(
    <horizontal>
        <button w="200" text="Width 200dp"/>
        <button w="100" text="Width 100dp"/>
    </horizontal>
);
```

## h

The height of the View, shorthand for the `height` property. Possible values are `*`, `auto`, and specific numbers. `*` means the height will **try its best** to fill the parent layout, while `auto` means the height will automatically adjust based on the View's content (adaptive height).

If this property is not set, different widgets and layouts have different default heights, most of which are `auto`.

The height property can also specify a specific value, such as `h="20"`, `h="20px"`, etc. Without a unit, the default unit is dp. Other units include px (pixels), mm (millimeters), and in (inches). For more information about dimension units, see [Dimension Units: Dimension](#ui_尺寸的单位_Dimension).

## id

The id of the View, used to distinguish different widgets and layouts within an interface. An interface's id is usually unique within that interface — generally, no two Views share the same id. The id property is also the bridge connecting the XML layout and JavaScript code. In code, you can retrieve a View using its id and perform operations on it (set click actions, set properties, get properties, etc.). For example:

```
"ui";
ui.layout(
    <frame>
        <button id="ok" text="OK"/>
    </frame>
);
// Retrieve the button widget via ui.ok
toast(ui.ok.getText());
```

This example has a button widget "OK" with id "ok". We can use `ui.ok` in code to retrieve it, and then use the `getText()` function to get the button's text content.
Additionally, this example uses a frame layout because we only have one widget, making the simplest frame layout appropriate.

## gravity

The "gravity" of the View. Used to determine the position of the View's content relative to the View itself. Possible values:

* `left` — Align to the left
* `right` — Align to the right
* `top` — Align to the top
* `bottom` — Align to the bottom
* `center` — Center
* `center_vertical` — Center vertically
* `center_horizontal` — Center horizontally

For example, for a button widget, `gravity="right"` will make its text content align to the right. For example:

```
"ui";
ui.layout(
    <frame>
        <button gravity="right" w="*" h="auto" text="Right-aligned text"/>
    </frame>
);
```

The display effect is:

![ex-gravity](images/ex-gravity.png)

These values can be combined, for example `gravity="right|bottom"` will place the View's content in the bottom-right corner.

## layout_gravity

The "gravity" of the View within its layout. Used to determine the position of the View itself within its **parent layout**. The possible values are the same as for the gravity property. Note the distinction between this property and the gravity property.

```
"ui";
ui.layout(
    <frame w="*" h="*">
        <button layout_gravity="center" w="auto" h="auto" text="Centered button"/>
        <button layout_gravity="right|bottom" w="auto" h="auto" text="Bottom-right button"/>
    </frame>
);
```

In this example, we make the frame layout fill the entire screen. By setting `layout_gravity="center"` on the first button, we center it within the frame layout. By setting `layout_gravity="right|bottom"` on the second button, we place it in the bottom-right corner of the frame layout. The effect is shown below:

![ex-layout-gravity](images/ex-layout-gravity.png)

Note that the `layout_gravity` property does not always take effect — it depends on the type of layout. For example, you cannot make the first child widget in a horizontal layout align to the bottom (as that would contradict the nature of a horizontal layout itself).

## margin

`margin` is the spacing between a View and other Views (i.e., outer margin). The margin property includes four values:

* `marginLeft` — Left outer margin
* `marginRight` — Right outer margin
* `marginTop` — Top outer margin
* `marginBottom` — Bottom outer margin

The value of the margin property itself can be specified in three formats:

* `margin="marginAll"` — Sets all margins to the same value. For example, `margin="10"` means 10dp for left, right, top, and bottom.
* `margin="marginLeft marginTop marginRight marginBottom"` — Sets each margin individually. For example, `margin="10 20 30 40"` means left=10dp, top=20dp, right=30dp, bottom=40dp.
* `margin="marginHorizontal marginVertical"` — Sets horizontal and vertical margins. For example, `margin="10 20"` means left/right=10dp, top/bottom=20dp.

Here is an example to understand the meaning of margins:

```
"ui";
ui.layout(
    <horizontal>
        <button margin="30" text="30dp from all sides"/>
        <button text="Normal button"/>
    </horizontal>
);
```

The first button's `margin` property sets its margin to 30dp, meaning 30dp spacing from the horizontal layout and from the second button. The display effect is:

![ex1-margin](images/ex1-margin.png)

If we change `margin="30"` to `margin="10 40"`, the first button will have 10dp horizontal margins and 40dp vertical margins. The effect is:

![ex2-margin](images/ex2-margin.png)

For units used with the margin property, see [Dimension Units: Dimension](#ui_尺寸的单位_Dimension).

## marginLeft

The left outer margin of the View. If this property conflicts with a value set by the margin property, the later property takes precedence and the earlier one is ignored. For example, with `margin="20" marginLeft="10"`, the left margin is 10dp and the other margins are 20dp.

```
"ui";
ui.layout(
    <horizontal>
        <button marginLeft="50" text="50dp from left"/>
        <button text="Normal button"/>
    </horizontal>
);
```

The first button specifies a left margin of 50dp, so its distance from the left edge of its parent horizontal layout is 50dp. The effect is:

![ex-marginLeft](images/ex-marginLeft.png)

## marginRight

The right outer margin of the View. If this property conflicts with a value set by the margin property, the later property takes precedence.

## marginTop

The top outer margin of the View. If this property conflicts with a value set by the margin property, the later property takes precedence.

## marginBottom

The bottom outer margin of the View. If this property conflicts with a value set by the margin property, the later property takes precedence.

## padding

The spacing between the View and its own content (i.e., inner padding). Note the difference from the margin property: margin is the spacing *between* Views, while padding is the spacing between a View and its own content. For example, the padding of a text widget is the distance between the widget's edges and its text content. `paddingLeft` is the distance between the left edge of the text widget and its text content.

The padding property supports the same three value formats:

* `padding="paddingAll"` — Sets all inner margins to the same value. For example, `padding="10"` means 10dp for left, right, top, and bottom.
* `padding="paddingLeft paddingTop paddingRight paddingBottom"` — Sets each padding individually. For example, `padding="10 20 30 40"`.
* `padding="paddingHorizontal paddingVertical"` — Sets horizontal and vertical padding. For example, `padding="10 20"`.

Here is an example to understand padding:

```
"ui";
ui.layout(
    <frame w="*" h="*" gravity="center">
        <text padding="10 20 30 40" bg="#ff0000" w="auto" h="auto" text="HelloWorld"/>
    </frame>
);
```

This example shows a centered text widget (using the parent layout's `gravity="center"`), with a red background (`bg="#ff0000"`), text content "HelloWorld", left padding 10dp, top padding 20dp, bottom padding 30dp, right padding 40dp. The effect is:

![ex-padding](images/ex-padding.png)

## paddingLeft

The left inner padding of the View. If this property conflicts with a value set by the padding property, the later property takes precedence.

## paddingRight

The right inner padding of the View. If this property conflicts with a value set by the padding property, the later property takes precedence.

## paddingTop

The top inner padding of the View. If this property conflicts with a value set by the padding property, the later property takes precedence.

## paddingBottom

The bottom inner padding of the View. If this property conflicts with a value set by the padding property, the later property takes precedence.

## bg

The background of the View. Its value can be an image referenced by a link or path, an RGB color, or other background types. See [Drawables](#draw) for details.

For example, `bg="#00ff00"` sets a green background, `bg="file:///sdcard/1.png"` sets the background to the image "1.png", and `bg="?attr/selectableItemBackground"` sets a ripple effect on click (you may also need to set `clickable="true"` for it to take effect).

## alpha

The opacity of the View. The value is a decimal between 0 and 1. 0 means fully transparent, 1 means fully opaque. For example, `alpha="0.5"` means semi-transparent.

## foreground

The foreground of the View. The foreground is content displayed on top of the View's own content and may cover it. Its value is similar to the `bg` property.

## minHeight

The minimum height of the View. This value does not always take effect — it depends on whether the parent layout has enough space.

Example: `<text height="auto" minHeight="50"/>`

For units, see [Dimension Units: Dimension](#ui_尺寸的单位_Dimension).

## minWidth

The minimum width of the View. This value does not always take effect — it depends on whether the parent layout has enough space.

Example: `<input width="auto" minWidth="50"/>`

For units, see [Dimension Units: Dimension](#ui_尺寸的单位_Dimension).

## visibility

The visibility of the View. This property determines whether the View is shown. Possible values:

* `gone` — Invisible (and does not take up space).
* `visible` — Visible. By default, Views are visible.
* `invisible` — Invisible, but still occupies space.

## rotation

The rotation angle of the View. This property allows the View to be rotated clockwise by a certain angle. For example, `rotation="90"` rotates it 90 degrees clockwise.

To set the rotation center, use the `transformPivotX` and `transformPivotY` properties. The default rotation center is the center of the View.

## transformPivotX

The x-coordinate of the View's transformation pivot. Used as the center for rotation, scaling, and other transformations. For example, `transformPivotX="10"`.

The coordinate system has its origin at the top-left corner of the View. That is, the x value is the distance from the transformation center to the left edge of the View.

For units, see [Dimension Units: Dimension](#ui_尺寸的单位_Dimension).

## transformPivotY

The y-coordinate of the View's transformation pivot. Used as the center for rotation, scaling, and other transformations. For example, `transformPivotY="10"`.

The coordinate system has its origin at the top-left corner of the View. That is, the y value is the distance from the transformation center to the top edge of the View.

For units, see [Dimension Units: Dimension](#ui_尺寸的单位_Dimension).

## style

Sets the style of the View. Different controls have different optional built-in styles. See the documentation for each control for details.

Note that the style property is only supported on Android 5.1 and above.

# Text Widget: text

The text widget is used to display text. You can control the font size, font color, font, etc.

The following introduces the main properties and methods of this widget. To see all its properties and methods, please read the [TextView](http://www.zhdoc.net/android/reference/android/widget/TextView.html) documentation.

## text

Sets the content of the text. For example, `text="some text"`.

## textColor

Sets the font color. Can be an RGB color (e.g. #ff00ff) or a color name (e.g. red, green, etc.). See [Colors](#ui_颜色) for details.

Example, red text: `<text text="red text" textColor="red"/>`

## textSize

Sets the font size. The unit is generally sp. According to Material Design guidelines, body text is 14sp, titles are 18sp, and subtitles are 16sp.

Example, extra large font: `<text text="extra large font" textSize="40sp"/>`

## textStyle

Sets the font style, such as italic, bold, etc. Possible values:

* bold — Bold font
* italic — Italic font
* normal — Normal font

You can combine them with "|" (pipe), for example bold italic is "bold|italic".

Example, bold: `<text textStyle="bold" textSize="18sp" text="This is bold"/>`

## lines

Sets the number of lines for the text widget. Even if the text content does not reach the set number of lines, the widget will reserve space to display blank lines. If the text content exceeds the set number of lines, the excess will not be displayed.

Also, multi-line text cannot be set directly in XML; it must be set in code. For example:

```
"ui";
ui.layout(
    <vertical>
        <text id="myText" lines="3">
    </vertical>
)
// Use \n for line breaks
ui.myText.setText("First line\nSecond line\nThird line\nFourth line");
```

## maxLines

Sets the maximum number of lines for the text widget.

## typeface

Sets the font. Possible values:

* `normal` — Normal font
* `sans` — Sans-serif font
* `serif` — Serif font
* `monospace` — Monospace font

Example, monospace font: `<text text="monospace font" typeface="monospace"/>`

## ellipsize

Sets the position of the ellipsis for the text. The ellipsis appears when the text content exceeds the text widget. Possible values:

* `end` — Show ellipsis at the end of the text
* `marquee` — Marquee effect, text will scroll
* `middle` — Show ellipsis in the middle of the text
* `none` — Do not show ellipsis
* `start` — Show ellipsis at the beginning of the text

## ems

When this property is set, the TextView displays a character length (in em units). Excess content will not be shown or will display an ellipsis according to the ellipsize setting.

Example, limit text to a maximum of 5em: `<text ems="5" ellipsize="end" text="a very very very very very very very long text"/>`

## autoLink

Controls whether URLs, email addresses, and other links are automatically detected and converted into clickable links. The default value is "none".

Setting this value makes links, phone numbers, etc. in the text become clickable.

Possible values are any combination of the following joined by "|":

* `all` — Match all links, emails, addresses, phones
* `email` — Match email addresses
* `map` — Match map addresses
* `none` — Do not match (default)
* `phone` — Match phone numbers
* `web` — Match URLs

Example: `<text autoLink="web|phone" text="Baidu: http://www.baidu.com Telecom: 10000"/>`

# Button Widget: button

The button widget is a special text widget, so all properties and functions of the text widget also apply to the button widget.

In addition, the button widget has some built-in styles that can be set via the `style` property, including:

* Widget.AppCompat.Button.Colored — Colored button
* Widget.AppCompat.Button.Borderless — Borderless button
* Widget.AppCompat.Button.Borderless.Colored — Colored borderless button

For the specific effects of these styles, see the example "示例/界面控件/按钮控件.js".

Example: `<button style="Widget.AppCompat.Button.Colored" text="Nice button"/>`

# Input Widget: input

The input widget is also a special text widget, so all properties and functions of the text widget also apply to the input widget. The input widget has its own properties and functions. To see all of them, read the [EditText](http://www.zhdoc.net/android/reference/android/widget/EditText.html) documentation.

For an input widget, we can set its content via the text property and specify the number of lines via the lines property. In code, we can get the input content via the `getText()` function. For example:

```
"ui";
ui.layout(
    <vertical padding="16">
        <text textSize="16sp" textColor="black" text="Please enter your name"/>
        <input id="name" text="Xiao Ming"/>
        <button id="ok" text="OK"/>
    </vertical>
);
// Specify the action to execute when the OK button is clicked
ui.ok.click(function(){
    // Get the input content via getText()
    var name = ui.name.getText();
    toast(name + " hello!");
});
```

The effect is shown below:

![ex-input](ex-input.png)

In addition, the input widget has some other main properties (although these properties are also available for text widgets, they are generally only used for input widgets):

## hint

Input hint. This hint is displayed when the input field is empty. As shown in the image:

![ex-hint](images/ex-hint.png)

The code for the above image effect is:

```
"ui";
ui.layout(
    <vertical>
        <input hint="Please enter your name"/>
    </vertical>
)
```

## textColorHint

Specifies the font color of the input hint.

## textSizeHint

Specifies the font size of the input hint.

## inputType

Specifies the type of text that can be entered in the input field. Possible values are any combination of the following joined by "|":

* `date` — For entering dates.
* `datetime` — For entering date and time.
* `none` — No content type. This input field is not editable.
* `number` — Only numbers can be entered.
* `numberDecimal` — Can be combined with number and its other options to allow decimal numbers (including fractions).
* `numberPassword` — Only numeric passwords can be entered.
* `numberSigned` — Can be combined with number and its other options to allow signed numbers.
* `phone` — For entering a phone number.
* `text` — Just plain text.
* `textAutoComplete` — Can be combined with text and its other options to specify that this field will do its own auto-completion and interact appropriately with the input method.
* `textAutoCorrect` — Can be combined with text and its other options to request automatic text input correction.
* `textCapCharacters` — Can be combined with text and its other options to request capitalizing all characters.
* `textCapSentences` — Can be combined with text and its other options to request capitalizing the first character of each sentence.
* `textCapWords` — Can be combined with text and its other options to request capitalizing the first character of each word.
* `textEmailAddress` — For entering an email address.
* `textEmailSubject` — For entering the subject of an email.
* `textImeMultiLine` — Can be combined with text and its other options to indicate that although the regular text view should not be multi-line, the IME should provide multi-line support if possible.
* `textLongMessage` — For entering the content of a long message.
* `textMultiLine` — Can be combined with text and its other options to allow multi-line text in this field. If this flag is not set, the text field will be limited to a single line.
* `textNoSuggestions` — Can be combined with text and its other options to indicate that the input method should not show any dictionary-based word suggestions.
* `textPassword` — For entering a password.
* `textPersonName` — For entering a person's name.
* `textPhonetic` — For entering text that is the phonetic pronunciation, such as the pinyin name field in a contact entry.
* `textPostalAddress` — For entering a mailing address.
* `textShortMessage` — For entering the content of a short message.
* `textUri` — For entering a URI.
* `textVisiblePassword` — For entering a visible password.
* `textWebEditText` — For entering text in a web form.
* `textWebEmailAddress` — For entering an email address in a web form.
* `textWebPassword` — For entering a password in a web form.
* `time` — For entering time.

For example, to specify that an input field accepts decimal numbers: `<input inputType="number|numberDecimal"/>`

## password

Specifies whether the input field is a password input field. Default is `false`.

Example: `<input password="true"/>`

## numeric

Specifies whether the input field is a numeric input field. Default is `false`.

Example: `<input numeric="true"/>`

## phoneNumber

Specifies whether the input field is a phone number input field. Default is `false`.

Example: `<input phoneNumber="true"/>`

## digits

Specifies the characters that can be entered in the input field. For example, to restrict input to only "1234567890+-": `<input digits="1234567890+-"/>`.

## singleLine

Specifies whether the input field is a single-line input field. Default is `false`. You can also use `lines="1"` to specify a single-line input field.

Example: `<input singleLine="true"/>`

# Image Widget: img

The image widget is used to display images from the network, local files, or embedded data. It can also display the image as a rounded rectangle, circle, etc. However, it cannot display animated GIFs.

Only the main methods and properties are introduced here. To see all methods and properties, read [ImageView](http://www.zhdoc.net/android/reference/android/widget/ImageView.html).

## src

Uses a Uri to specify the image source. It can be an image URL (http://....), a local path (file://....), or base64 data ("data:image/png;base64,...").

If an image URL or local path is used, Auto.js will automatically use appropriate caching to store the images and reduce loading time on subsequent loads.

Example, displaying Baidu's logo:

```
"ui";
ui.layout(
    <frame>
        <img src="https://www.baidu.com/img/bd_logo1.png"/>
    </frame>
);
```

Another example, displaying the image file at /sdcard/1.png: `<img src="file:///sdcard/1.png"/>`.
Another example, displaying a small wallet image via base64:

```
"ui";
ui.layout(
    <frame>
        <img w="40" h="40" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADwAAAA8CAYAAAA6/NlyAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAEu0lEQVRoge3bW4iVVRQH8N+ZnDKxvJUGCSWUlXYle/ChiKAkIiu7UXQjonwNIopM8cHoAhkRGQXdfIiE0Ep8KalQoptRTiFFZiRlOo6TPuSk4zk97G9w5vidc77LPjNi84f1MN+391rrf9a+rL32N4xiFMcUjouo5zyciYPYH0FnBadiNiZiD2oR9JbGRdgiOFPDIXRhCWYU0Dcj6duV6BrQuyWxNaLowBcOO1Uv+7EKc4WINUIlabMq6dNI35eJzRHDWOzS2MEB6cd6XI/OQf07k2frkzat9HQnNkcUG7R2dECq2I53EtmePMvaf+MwcWqKu+RzuqhUcfcwcWqKTvmiXFQ2GDodRhQz0aN9ZHsSG0cVrkGf+GT7MG8YeeTCHeKS7sOdMR1stjcWxY2YH0nXh1gdSdf/E+2I8KVYigkl9ewVUsxNpT1qMzaKN4ejJxrtyEt7IuraE1EX2jOkp+JBnFxSzz68KuTqoyiK2BHuxDO4NpK+j/GoOAWF6BiH98Q/SHyCycPIIxMm4FPZCPTj30SynIFr+A7ThotMK4wXopA1Ym9gSiKv5Oj3bdKnFMpuS514E1fm6NMnbF098s3NS4QS0Ik5+hyBsoSXYkGO9jvxy6C/t+IPIYJZcBWW57AXFfMNrSo2kqqw2l4hvSzcIRTw1sm24FVxb5s4NcR0/JXBuUNYJttI6sDjsi1kvTgrGpsMjq3O4FQNa+SbNhWsyKj7I4wpzSYDbpFtKB/EOSn9ZwpRfx5Xp7yfhN0Z9FdxXxxKjTEe2zI4U8NnKf3PNrT2VcWTKe1eyGjjT+Eapm14IqMjNTyd0n9JSrsDwhmaEN2H8GMOO8viUjyMSfJVJh9O0bGoQdt1eFm2oVwve7UpC1ssX568KEXH6fghp54s8lRkrk7CjpxOrGqg6wQ8IKSKWXPpVtIt8ly+v4ATf2t+yqlgDl5SbCjXy8JIXFXweQEHqngxo43JeEw54l+JVLKaJeypRZzoFxavrIWG6cKPW2SO9+PCMkQHsLiA8fpIv5/DmUn4qaCtpWWIEiLzdUHj9XJA2H5uFRbBZriuoI1NSpatpio+nJtFvFvYd2c1sDsGvxfQ3a/knrwgMtm0qD8rPSprCuq8uRmhVqvanBbvm+EQfsNKIcnvTmnTiUdwQcq73oJ2L2v2stXx6vyCRr8RDuk/C8OMUK24J6VtBaekPG81zxuh0TTJhC7FhtUOHF+n61whGalvu8uRWVJFvgPEYOkqQzhLVSPPXLoYa4Xh3Stcls1NaTdb8Xx7ZxnCvSUIfy/kzWno0Pyzx3dL2C0695Hto7NGUhXy5Lzp3kLZKiqNpNTl2+YShgdIvyXbVck44TB/oKTNzWUIv13S+IDsFmpY84QvZAcwTbh4e04o18SwtbIM4dsiOTFYVgzSv7wN+m9vRqjV/PrA0JuCox1bhYNKQ7Qi3CcU1fpiedRG9AkLXhRfbxCnKlET0s21ifwaSWcPbopBdDDOwGtClTD2vCsq+/C68K8HmVDk7DhFyIsvFzKnGThN+689+oU9dptwQb5B+LB8dx4lMb7xqAhkJwo/xljhFFSfSdUc3mPrcbwj15P+pP0/QiR7hYSkGsHnUYziWMF/mXV4JVcZ8G0AAAAASUVORK5CYII="/>
    </frame>
);
```

## tint

Image tinting. The value is a color name or RGB color value. Using this property will paint all non-transparent areas of the image with the same color. Useful for changing the color of an image.

For example, for the base64 image above: `<img w="40" h="40" tint="red" src="data:image/png;base64,..."/>` will turn the wallet icon red.

## scaleType

Controls how the image is scaled to fit the width and height of the image widget. Available values:

* `center` — Center the image inside the widget without scaling it.
* `centerCrop` — Scale the image while preserving aspect ratio so its dimensions (width and height) are equal to or larger than the widget's (excluding padding) and center it inside the widget.
* `centerInside` — Scale the image while preserving aspect ratio so its dimensions (width and height) are smaller than or equal to the widget's (excluding padding) and center it inside the widget.
* `fitCenter` — Scale the image while preserving aspect ratio so that its width **or** height matches the widget's and center it.
* `fitEnd` — Scale the image while preserving aspect ratio so that its width **or** height matches the widget's and align it to the bottom-right corner.
* `fitStart` — Scale the image while preserving aspect ratio so that its width **or** height matches the widget's and align it to the top-left corner.
* `fitXY` — Stretch the image to exactly fill the widget's width and height (aspect ratio may not be preserved).
* `matrix` — Use a custom image matrix for scaling during drawing. Requires calling `setImageMatrix(Matrix)` in code to take effect.

The default scaleType is `fitCenter`. Besides that, `fitXY` is the most commonly used — it scales the image to exactly the size of the widget, but the image may appear distorted.

## radius

The radius of the image widget. If set to half the width and height of the widget and the width equals the height, the image will be clipped as a circle; otherwise it will be displayed as a rounded rectangle. The radius is the radius of the four rounded corners. You can also set the four corner radii individually using `radiusTopLeft`, `radiusTopRight`, `radiusBottomLeft`, `radiusBottomRight`.

Example, rounded rectangle Auto.js icon: `<img w="100" h="100" radius="20" bg="white" src="http://www.autojs.org/assets/uploads/profile/3-profileavatar.png" />`

For the unit of this property, see [Dimension Units: Dimension](#ui_dimension-units-dimension).

## radiusTopLeft

The top-left corner radius of the image widget. For the unit of this property, see [Dimension Units: Dimension](#ui_dimension-units-dimension).

## radiusTopRight

The top-right corner radius of the image widget. For the unit of this property, see [Dimension Units: Dimension](#ui_dimension-units-dimension).

## radiusBottomLeft

The bottom-left corner radius of the image widget. For the unit of this property, see [Dimension Units: Dimension](#ui_dimension-units-dimension).

## radiusBottomRight

The bottom-right corner radius of the image widget. For the unit of this property, see [Dimension Units: Dimension](#ui_dimension-units-dimension).

## borderWidth

The border width of the image widget. Used to display a border around the image; the border will change accordingly with the shape of the image widget (rounded corners, etc.).
Example, rounded rectangle Auto.js icon with gray border: `<img w="100" h="100" radius="20" borderWidth="5" borderColor="gray" bg="white" src="http://www.autojs.org/assets/uploads/profile/3-profileavatar.png" />`

## borderColor

The border color of the image widget.

## circle

Specifies whether the image of this image widget should be clipped to a circle. If `true`, the image widget will keep its width and height equal (if they are not equal, height will be set equal to width) and the circle's radius will be half the width.

Example, circular Auto.js icon: `<img w="100" h="100" circle="true" bg="white" src="http://www.autojs.org/assets/uploads/profile/3-profileavatar.png" />`

# Vertical Layout: vertical

A vertical layout is a relatively simple layout that arranges the widgets inside it sequentially in the vertical direction, as shown below:

Vertical layout:

—————

| Widget 1 |

| Widget 2 |

| Widget 3 |

| ............ |

——————

## layout_weight

Widgets inside a vertical layout can use the `layout_weight` property to control what proportion of the vertical layout's height the widget occupies. If `layout_weight` is specified for a widget, then its height = (remaining height of the vertical layout) × layout_weight / weightSum. If weightSum is not specified, weightSum is the sum of the layout_weight values of all child widgets. "Remaining height" refers to the height left in the vertical layout after subtracting the heights of widgets that did not specify layout_weight.
Example:

```
"ui";
ui.layout(
    <vertical h="100dp">
        <text layout_weight="1" text="Widget 1" bg="#ff0000"/>
        <text layout_weight="1" text="Widget 2" bg="#00ff00"/>
        <text layout_weight="1" text="Widget 3" bg="#0000ff"/>
    </vertical>
);
```

In this layout, all three widgets have layout_weight of 1, meaning each will occupy 1/3 of the vertical layout's height, i.e. 33.3dp.
Another example:

```
"ui";
ui.layout(
    <vertical h="100dp">
        <text layout_weight="1" text="Widget 1" bg="#ff0000"/>
        <text layout_weight="2" text="Widget 2" bg="#00ff00"/>
        <text layout_weight="1" text="Widget 3" bg="#0000ff"/>
    </vertical>
);
```

In this layout, the first widget is 1/4 height, the second is 2/4, and the third is 1/4.
Another example:

```
"ui";
ui.layout(
    <vertical h="100dp" weightSum="5">
        <text layout_weight="1" text="Widget 1" bg="#ff0000"/>
        <text layout_weight="2" text="Widget 2" bg="#00ff00"/>
        <text layout_weight="1" text="Widget 3" bg="#0000ff"/>
    </vertical>
);
```

In this layout, because weightSum is specified as 5, the first widget is 1/5, the second is 2/5, and the third is 1/5.
Another example:

```
"ui";
ui.layout(
    <vertical h="100dp">
        <text h="40dp" text="Widget 1" bg="#ff0000"/>
        <text layout_weight="2" text="Widget 2" bg="#00ff00"/>
        <text layout_weight="1" text="Widget 3" bg="#0000ff"/>
    </vertical>
);
```

In this layout, the first widget did not specify layout_weight but instead specified a fixed height of 40dp, so it is excluded from the proportion calculation. The remaining height of the layout is therefore 60dp. The second widget takes 2/3 of the remaining height (40dp), and the third takes 1/3 of the remaining height (20dp).

The layout_weight property of a vertical layout can also be used to make a child widget fill the remaining space, for example:

```
"ui";
ui.layout(
    <vertical h="100dp">
        <text h="40dp" text="Widget 1" bg="#ff0000"/>
        <text h="40dp" text="Widget 2" bg="#00ff00"/>
        <text layout_weight="1" text="Widget 3" bg="#0000ff"/>
    </vertical>
);
```

In this layout, the third widget's height will fill all remaining space after Widget 1 and Widget 2.

# Horizontal Layout: horizontal

A horizontal layout is a relatively simple layout that arranges the widgets inside it sequentially from left to right, as shown below:
Horizontal layout:
————————————————————————————

| Widget 1 | Widget 2 | Widget 3 | ... |

————————————————————————————

## layout_weight

The layout_weight property can also be used in a horizontal layout to control the **width** proportion of child widgets relative to the parent layout. It works similarly to the vertical layout and will not be repeated here.

# Linear Layout: linear

In fact, both vertical and horizontal layouts belong to linear layouts. A linear layout has an `orientation` property that specifies the direction of the layout. Possible values are `vertical` and `horizontal`.

For example `<linear orientation="vertical"></linear>` is equivalent to `<vertical></vertical>`.

The default orientation of a linear layout is horizontal. Therefore, a linear layout without the orientation attribute specified is a horizontal layout.

# Frame Layout: frame

Frame layout

# Relative Layout: relative

# Checkbox Widget: checkbox

# Radio Button Widget: radio

# Radio Group Layout: radiogroup

# Switch Widget: Switch

The switch widget is used to indicate whether an option is selected.

## checked

Indicates whether the switch is on. Possible values:

* `true` — turn the switch on
* `false` — turn the switch off

## text

Text describing the switch.

# Progress Bar Widget: progressbar

# Seek Bar Widget: seekbar

# Spinner (Dropdown Menu) Widget: spinner

# Time Picker Widget: timepicker

# Date Picker Widget: datepicker

# Floating Action Button Widget: fab

# Toolbar Widget: toolbar

# Card: card

The card widget is a control with rounded corners and shadow.

## cardBackgroundColor

The background color of the card.

## cardCornerRadius

The corner radius of the card.

## cardElevation

Sets the elevation of the card on the z-axis to control the size of the shadow.

## contentPadding

Sets the inner padding of the card. This property includes four values:

* `contentPaddingLeft` — left padding
* `contentPaddingRight` — right padding
* `contentPaddingTop` — top padding
* `contentPaddingBottom` — bottom padding

## foreground

Using the `foreground="?selectableItemBackground"` property can add a click effect to the card.

# Drawer Layout: drawer

# List: list

# Tab: tab

# ui

## ui.layout(xml)

* `xml` {XML} | {string} Layout XML or XML string

Renders the layout XML into a View object and sets it as the current view.

## ui.layoutFile(xmlFile)

* `xmlFile` {string} Path to the layout XML file

此函数和`ui.layout`相似, 只不过允许传入一个xml文件路径来渲染布局.

## ui.inflate(xml[, parent = null, attachToParent = false])

* `xml` {string} | {XML} 布局XML或者XML字符串
* `parent` {View} 父视图
* `attachToParent` {boolean} 是否渲染的View加到父视图中, 默认为false
* 返回 {View}

将布局XML渲染为视图（View）对象. 如果该View将作为某个View的子View, 我们建议传入`parent`参数, 这样在渲染时依赖于父视图的一些布局属性能够正确应用.

此函数用于动态创建、显示View.

```javascript
"ui";

$ui.layout(
    <linear id="container">
    </linear>
);

// 动态创建3个文本控件, 并加到container容器中
// 这里仅为实例, 实际上并不推荐这种做法, 如果要展示列表, 
// 使用list组件；动态创建十几个、几十个View会让界面卡顿
for (let i = 0; i < 3; i++) {
    let textView = $ui.inflate(
        <text textColor="#000000" textSize="14sp"/>
    , $ui.container);
    textView.attr("text", "文本控件" + i);
    $ui.container.addView(textView);
}
```

# ui.registerWidget(name, widget)

* `name` {string} 组件名称
* `widget` {Function} 组件

注册一个自定义组件. 参考示例->界面控件->自定义控件.

# ui.isUiThread()

* 返回 {boolean}

返回当前线程是否是UI线程.

```javascript
"ui";

log($ui.isUiThread()); // => true

$threads.start(function () {
    log($ui.isUiThread()); // => false
});

```

## ui.findView(id)

* `id` {string} View的ID
* 返回 {View}

在当前视图中根据ID查找相应的视图对象并返回. 如果当前未设置视图或找不到此ID的视图时返回`null`.

一般我们都是通过`ui.xxx`来获取id为xxx的控件, 如果xxx是一个ui已经有的属性, 就可以通过`$ui.findView()`来获取这个控件.

## ui.finish()

结束当前活动并销毁界面.

## ui.setContentView(view)

* `view` {View}

将视图对象设置为当前视图.

## ui.post(callback[, delay = 0])

* `callback` {Function} 回调函数
* `delay` {number} 延迟, 单位毫秒

将`callback`加到UI线程的消息循环中, 并延迟delay毫秒后执行（不能准确保证一定在delay毫秒后执行）.

此函数可以用于UI线程中延时执行动作（sleep不能在UI线程中使用）, 也可以用于子线程中更新UI.

```javascript
"ui";

ui.layout(
    <frame>
        <text id="result"/>
    </frame>
);

ui.result.attr("text", "计算中");
// 在子线程中计算1+ ... + 10000000
threads.start({
    let sum = 0;
    for (let i = 0; i < 1000000; i++) {
        sum += i;
    }
    // 由于不能在子线程操作UI, 所以要抛到UI线程执行
    ui.post(() => {
        ui.result.attr("text", String(sum));
    });
});
```

## ui.run(callback)

* `callback` {Function} 回调函数
* 返回 callback的执行结果

将`callback`在UI线程中执行. 如果当前已经在UI线程中, 则直接执行`callback`；否则将`callback`抛到UI线程中执行（加到UI线程的消息循环的末尾）, **并等待callback执行结束(阻塞当前线程)**.

## ui.statusBarColor(color)

* color {string} | {number} 颜色

设置当前界面的状态栏颜色.

```javascript
"ui";
ui.statusBarColor("#000000");
```

## ui.useAndroidResources()

启用使用Android的布局(layout)、绘图(drawable)、动画(anim)、样式(style)等资源的特性. 启用该特性后, 在project.json中进行以下配置, 就可以像写Android原生一样写界面：

```json
{
    // ...
    androidResources: {
        "resDir": "res",  // 资源文件夹
        "manifest": "AndroidManifest.xml" // AndroidManifest文件路径
    }
}
```

res文件夹通常为以下结构：

```
- res
    - layout  // 布局资源
    - drawable // 图片、形状等资源
    - menu // 菜单资源
    - values // 样式、字符串等资源
    // ...
```

可参考示例->复杂界面->Android原生界面.

# 尺寸的单位: Dimension

# Drawables

# 颜色

**(完善中...)**
