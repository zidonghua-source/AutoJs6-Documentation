# Q & A

---

## AutoJs6

### Introduction to AutoJs6 Features

AutoJs6 is a JavaScript automation tool for the Android platform that supports the Accessibility service.

It can be used as a JavaScript IDE, supporting features such as [code completion / variable renaming / code formatting], etc.

AutoJs6 bundles a rich set of JavaScript modules that provide extensive functionality along with many built-in utilities:

**Features**

- Image processing / Text recognition (OCR)
- Automation operations / Control operations / App operations
- UI interaction / Dialog interaction / Floating window controls / Canvas controls
- Multithreaded programming / Coroutines / Asynchronous programming / Event listeners
- File handling / Multimedia processing
- Scheduled tasks / Notifications
- HTTP requests
- Shell commands
- Internationalization
- ... and more

**Utilities**

- Device information / Sensor information / Control information
- Base64 encoding/decoding / Cryptography
- Mathematical operations / Color conversion
- ... and more

### How to Use AutoJs6

See the [AutoJs6 User Manual](manual) chapter for details.

### Is AutoJs6 Free?

AutoJs6 is permanently free. It is a secondary development based on the open-source version (Auto.js 4.1.1 alpha2) and will remain open-source and free.

### Goals of AutoJs6

The open-source version (Auto.js 4.1.1 alpha2) is excellent learning material. AutoJs6 exists precisely because it stands on the shoulders of giants.

The goal of AutoJs6 is to improve and extend the open-source version (Auto.js 4.1.1 alpha2).

### Highlights of AutoJs6

AutoJs6 has put significant effort into polishing the following features:

- Dark mode (night mode)
- Multi-language support

At the same time, existing modules have been carefully optimized and extended:

- [Color (colors)](color)
- [Selector (UiSelector)](uiSelectorType)
- [Control Node (UiObject)](uiObjectType)
- ... and more

Particularly characteristic of AutoJs6 are the [pickup selector](uiSelectorType#m-pickup) and the [compass control](uiObjectType#m-compass).

For more information about AutoJs6, see the [Project Changelog](http://changelog.autojs6.com).

## Documentation

### Inconsistent Documentation Format

The AutoJs6 documentation is built by updating and modifying the original open-source version's documentation. Currently, only some chapters have been updated. Unupdated chapters still retain the original content, resulting in a mix of old and new documentation styles.

Because writing documentation requires a huge amount of time and effort, the update speed is relatively slow. Once all chapters are written and updated, the documentation format will be unified.

### Night Mode Not Working

When viewing the documentation in AutoJs6 with night mode enabled, the docs may still appear in a light theme. Check the version requirements for WebView (or Google Chrome, etc.):

- API level 29 (Android 10) [Q] and above: version 76 or higher
- API level 28 (Android 9) [P] and below: version 105 or higher

### Content Is Hard to Understand

If you find certain documentation content difficult to understand, try skipping it temporarily and continue reading the following sections. After fully reading a chapter or section, you may gain a better understanding of the previously skipped content.

You can also submit feedback on the GitHub project page. Developers may adjust the documentation content based on the feedback received.

## Images

### OCR Feature

AutoJs6's OCR feature is implemented based on [Google ML Kit](https://developers.google.com/ml-kit) [Text Recognition API](https://developers.google.com/ml-kit/vision/text-recognition/android) and [Baidu PaddlePaddle](https://www.paddlepaddle.org.cn/)'s [Paddle Lite](https://github.com/PaddlePaddle/Paddle-Lite).

> Note:  
> The [OCR implementation source code](http://project.autojs6.com/blob/master/app/src/main/java/org/autojs/autojs/runtime/api/OcrMLKit.kt) for AutoJs6 based on the MLKit engine references the [Auto.js](https://github.com/TonyJiangWJ/Auto.js) project by [TonyJiangWJ](https://github.com/TonyJiangWJ).  
> The [OCR implementation source code](http://project.autojs6.com/blob/master/app/src/main/java/org/autojs/autojs/runtime/api/OcrPaddle.kt) for AutoJs6 based on the Paddle Lite engine comes from a [GitHub PR](http://pr.autojs6.com/120) by [TonyJiangWJ](https://github.com/TonyJiangWJ).

> See also: [Optical Character Recognition (OCR)](ocr) module

### Region Capture (Partial Screenshot)

AutoJs6 does not support region capture (partial screenshots).

You can use [images.captureScreen](image#m-capturescreen) to capture the full screen and then use methods such as [images.clip](image#m-clip) for further processing.

## Scheduled Tasks

### Running Scripts on a Schedule

From the script's right-click menu → Scheduled Tasks, you can set up scheduled execution.  
AutoJs6 must be allowed to run in the background, including being added to the [autostart whitelist / battery optimization ignore list / background activity restriction ignore list / system task retention list], etc.

When the device screen is off, you can use `device.wakeUp()` to wake the screen.  
However, AutoJs6 does not currently provide an unlock feature, so you may need to implement unlock logic yourself depending on the device.

### Passing External Parameters to Scheduled Tasks

If a script is started by an intent (such as a network status change or other specific event), you can obtain the intent via `engines.myEngine().execArgv.intent` and then extract external parameters from it.

## Script Execution Differences

The same script may produce different results or even fail with exceptions when run in different environments (different devices, systems, etc.).

### Different System Versions

AutoJs6 can be installed on operating systems with `Android API 24 (7.0) [N]` and above.

However, different operating systems have differences in `API` availability. Some `API`s only become available (or become unavailable) after a certain system version.

Here are some methods or properties in AutoJs6 that are affected by system version:

- Channel-related features in the [notice](notice) module only work on `Android API 26 (8.0) [O]` and above
- [device.imei](device#p-imei) can only retrieve the device IMEI on `Android API 29 (10) [Q]` and below
- [UiSelector#imeEnter](uiSelectorType#m-imeenter) only works on `Android API 30 (11) [R]` and above
- [UiSelector#dragStart](uiSelectorType#m-dragstart) only works on `Android API 32 (12.1) [S_V2]` and above
- [UiSelector#showTextSuggestions](uiSelectorType#m-showtextsuggestions) only works on `Android API 33 (13) [TIRAMISU]` and above
- ... and more

### Different Device Manufacturers

Because different manufacturers customize and modify the operating system to varying degrees, some `API`s may behave differently or be changed.

The table below lists some manufacturers and their operating systems (in no particular order):

| Manufacturer / Brand                     | Operating System              |
|------------------------------------------|-------------------------------|
| Meizu (MEIZU)                            | Flyme OS                      |
| OPPO / Realme                            | ColorOS                       |
| Xiaomi (XiaoMi / Redmi / BlackShark)     | MIUI                          |
| OnePlus                                  | Hydrogen OS / Oxygen OS       |
| VIVO / iQOO                              | Funtouch OS / OriginOS        |
| Huawei / Honor                           | EMUI / HarmonyOS              |
| Lenovo                                   | ZUI                           |
| Coolpad                                  | CoolOS                        |
| Droi                                     | Freeme OS                     |
| Smartisan                                | Smartisan OS                  |
| ZTE / Axon                               | MyOS                          |
| Nubia / Red Magic                        | REDMAGIC OS                   |
| Google Pixel                             | Stock Android                 |
| AVD (Android Virtual Device)             | Stock Android                 |
| Sony (Sony / XPERIA)                     | Near-stock                    |
| Samsung                                  | Near-stock                    |
| BlackBerry                               | Near-stock                    |
| LG                                       | Near-stock                    |
| Motorola                                 | Near-stock                    |
| Nokia                                    | Near-stock (limited models)   |
| ASUS (ASUS / ZenFone / ROG Phone)        | Near-stock                    |
| HTC                                      | Near-stock                    |

As can be seen, achieving completely identical and exception-free script execution results across many different operating systems is extremely difficult.

It is often necessary to perform functional testing on actual devices and write additional compatibility code. In some cases, you may even need to consult the open `API` documentation of the customized operating system (if available).

> Note: The information in the table may differ from reality and is for reference only.

### Different Auto.js Applications

Different Auto.js applications have added, modified, or removed [JavaScript wrapper modules / Java package and class names], etc., to varying degrees. Therefore, the same script is unlikely to achieve identical results across different Auto.js apps and may even fail to run.

Possible solutions:

- Continue using the Auto.js application with which you originally wrote the scripts
- Modify the script code to adapt to the new Auto.js application
- Add detection for different Auto.js applications in your script and write compatibility code in the corresponding branches

### Different AutoJs6 Versions

As AutoJs6 versions are updated, some `API`s may be [added / modified / deprecated / removed].

After upgrading AutoJs6, if one or more `API`s behave unexpectedly, you can consult the documentation, locate the relevant chapter, and troubleshoot according to the documentation.

If the problem remains unresolved, submit [feedback](#feedback) on the project's GitHub Issues page.

## Packaging Applications

AutoJs6's packaging feature is still incomplete. Packaged apps may have significant functional and interface differences compared to the main AutoJs6 application.

AutoJs6 developers are not currently participating in packaging-related development work. Currently, [LZX284](https://github.com/LZX284) is the main contributor maintaining the packaging feature, with other developers continuing to contribute code.

### Packaging Images/Resources and Multiple Scripts Together

This requirement uses the "Project" feature.

Click the "+" icon on the AutoJs6 main page, select Project, fill in the information, and create a new project.  
Projects can store multiple [scripts / modules / resource files].  
Click the APK packaging icon in the project toolbar to package the project.

Example:  
Script reads `1.png` in the same directory: `images.read("./1.png")`.  
UI script image control references `2.png` in the same directory: `<img src="file://2.png"/>`.  
AutoJs6 built-in modules support relative path references. In other cases, you may need to use `files.path()` to convert to an absolute path.

### Packaged App Does Not Show Main Interface

Use the "Project" feature.  
After creating a new project, add the following entry to the `project.json` file in the project directory:

```json
{
  "launchConfig": {
    "hideLogs": true
  }
}
```

Example:

```json
{
  "name": "First-Project",
  "versionName": "1.0.0",
  "versionCode": 1,
  "packageName": "org.autojs.example.first",
  "main": "main.js",
  "launchConfig": {
    "hideLogs": true
  }
}
```

## Code Conversion

AutoJs6 supports directly calling [Java / Android / extension library] APIs, etc.  
For functionality not built into AutoJs6, you can perform Java scripting — that is, directly refer to Java (or Kotlin, etc.) source code and convert it into JavaScript code.

Example:

```java
import android.graphics.Bitmap;
import android.graphics.Matrix;

public static Bitmap rotate(Bitmap src, int degrees, float px, float py) {
    if (degrees == 0) return src;
    Matrix matrix = new Matrix();
    matrix.setRotate(degrees, px, py);
    Bitmap ret = Bitmap.createBitmap(src, 0, 0, src.getWidth(), src.getHeight(), matrix, true);
    return ret;
}
```

Converted to JavaScript:

```js
importClass(android.graphics.Bitmap);
importClass(android.graphics.Matrix);

function rotate(src, degrees, px, py) {
    if (degrees == 0) return src;
    let matrix = new Matrix();
    matrix.setRotate(degrees, px, py);
    let ret = Bitmap.createBitmap(src, 0, 0, src.getWidth(), src.getHeight(), matrix, true);
    return ret;
}
```

For more information about scripting Java, see the [Scripting Java](scriptingJava) chapter.

## Feedback

If you have any questions or suggestions, you can open a new issue on the GitHub project page.

For feedback regarding the **Application Documentation**:  
http://docs-issues.autojs6.com

For feedback regarding **AutoJs6** itself:  
http://issues.autojs6.com
