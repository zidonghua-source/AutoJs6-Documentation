# App

---

<p style="font: italic 1em sans-serif; color: #78909C">This chapter is to be supplemented or improved...</p>
<p style="font: italic 1em sans-serif; color: #78909C">Marked by SuperMonster003 on Oct 22, 2022.</p>

---

The `app` module provides a series of functions for launching other applications and interacting with them, such as sending intents, opening files, sending emails, etc.

It also provides convenient advanced functions `startActivity` and `sendBroadcast`, which can be used to accomplish interactions with other apps that are not built into the `app` module.

## app.versionCode

* {number}

The version code of the current application, an integer value (e.g. 160, 256, etc.).

If running in Auto.js, this is the version code of Auto.js; in a packaged application, this is the version code of the packaged app.

```js
toastLog(app.versionCode);
```

## app.versionName

* {string}

The version name of the current application (e.g. "3.0.0 Beta").

If running in Auto.js, this is the version name of Auto.js; in a packaged application, this is the version name of the packaged app.

```js
toastLog(app.versionName);
```

## app.autojs.versionCode

* {number}

Auto.js version code, an integer value (e.g. 160, 256, etc.).

## app.autojs.versionName

* {string}

Auto.js version name (e.g. "3.0.0 Beta").

## app.launchApp(appName)

* `appName` {string} Application name

Launches an application by its name. Returns `false` if no application with that name exists; otherwise returns `true`. If multiple applications match the name, only one will be launched.

This function can also be used as a global function.

```js
launchApp("Auto.js");
```

## app.launch(packageName)

* `packageName` {string} Application package name

Launches an application by its package name. Returns `false` if no application with that package name is installed; otherwise returns `true`.

This function can also be used as a global function.

```js
// Launch WeChat
launch("com.tencent.mm");
```

## app.launchPackage(packageName)

* `packageName` {string} Application package name

Equivalent to `app.launch(packageName)`.

## app.getPackageName(appName)

* `appName` {string} Application name

Gets the package name of an installed application by its name. Returns `null` if the application is not found. If multiple applications match the name, only one package name will be returned.

This function can also be used as a global function.

```js
var name = getPackageName("QQ"); // returns "com.tencent.mobileqq"
```

## app.getAppName(packageName)

* `packageName` {string} Application package name

Gets the name of an installed application by its package name. Returns `null` if the application is not found.

This function can also be used as a global function.

```js
var name = getAppName("com.tencent.mobileqq"); // returns "QQ"
```

## app.openAppSetting(packageName)

* `packageName` {string} Application package name

Opens the application's details page (settings page). Returns `false` if the application is not found; otherwise returns `true`.

This function can also be used as a global function.

## app.viewFile(path)

* `path` {string} File path

Opens a file using another application. If the file does not exist, it will be handled by the viewing application.

If no application capable of viewing the file can be found, an `ActivityNotFoundException` is thrown.

```js
// View a text file
app.viewFile("/sdcard/1.txt");
```

## app.editFile(path)

* `path` {string} File path

Opens a file for editing using another application. If the file does not exist, it will be handled by the editing application.

If no application capable of editing the file can be found, an `ActivityNotFoundException` is thrown.

```
// Edit a text file
app.editFile("/sdcard/1.txt");
```

## app.uninstall(packageName)

* `packageName` {string} Application package name

Uninstalls an application. A system prompt for uninstalling the app will appear after execution. If the application with the given package name is not installed, the uninstaller will handle it and may show a "Application not found" message.

```js
// Uninstall QQ
app.uninstall("com.tencent.mobileqq");
```

## app.openUrl(url)

* `url` {string} The URL of the website. If it does not start with "http://" or "https://", it defaults to "http://".

Opens the given URL in a browser.

If no browser application is installed, an `ActivityNotFoundException` is thrown.

## app.sendEmail(options)

* `options` {Object} Parameters for sending the email. Includes:
  * `email` {string} | {Array} Recipient email address(es). Use an array for multiple recipients.
  * `cc` {string} | {Array} CC recipient email address(es).
  * `bcc` {string} | {Array} BCC recipient email address(es).
  * `subject` {string} Email subject (title)
  * `text` {string} Email body
  * `attachment` {string} Path to the attachment.

Calls an email application to send mail according to the `options`. All options are optional.

If no email application is installed, an `ActivityNotFoundException` is thrown.

```js
// Send email to 10086@qq.com and 10001@qq.com
app.sendEmail({
    email: ["10086@qq.com", "10001@qq.com"],
    subject: "This is the email subject",
    text: "This is the email body"
});
```

## app.startActivity(name)

* `name` {string} Activity name. Possible values:
  * `console` - Console / log interface
  * `settings` - Settings interface

Launches a specific Auto.js interface. When run inside Auto.js, it opens the corresponding interface within Auto.js. When run in a packaged app, it opens the corresponding interface of the packaged application.

```js
app.startActivity("console");
```

## app.intent(options)

* `options` {Object} Options for constructing the Intent, including:
  * `action` {string} The Action of the intent — the action the intent should perform. It is a string constant such as `"android.intent.action.SEND"`. When the action starts with `"android.intent.action"`, the prefix can be omitted and `"SEND"` can be used directly. See [Actions](https://developer.android.com/reference/android/content/Intent.html#standard-activity-actions/).

  * `type` {string} The MimeType of the intent, indicating the type of data directly associated with the intent (e.g. `"text/plain"` for plain text).

  * `data` {string} The Data of the intent — a Uri representing the data associated with the intent (file path, URL, etc.). For example, to open a file: `action: "VIEW"`, `data: "file:///sdcard/1.txt"`.

  * `category` {Array} Categories of the intent. Less commonly used. See [Categories](https://developer.android.com/reference/android/content/Intent.html#standard-categories/).

  * `packageName` {string} Target package name

  * `className` {string} Name of the target Activity, Service, or other component

  * `extras` {Object} Extras (additional information) of the Intent as key-value pairs. Used to provide extra data, such as email subject and body when sending mail. See [Extras](https://developer.android.com/reference/android/content/Intent.html#standard-extra-data/).

  * `flags` {Array} Intent flags as an array of strings, e.g. `["activity_new_task", "grant_read_uri_permission"]`. See [Flags](https://developer.android.com/reference/android/content/Intent.html#setFlags(int)).

    **[Added in v4.1.0]**

  * `root` {boolean} Whether to start/send this intent with root privileges. When using this parameter, you should not use `context.startActivity()` etc., but call methods such as `app.startActivity({...})` directly.

    **[Added in v4.1.0]**

Constructs an Intent object based on the provided options.

Example:

```js
// Open an application to view an image file
var i = app.intent({
    action: "VIEW",
    type: "image/png",
    data: "file:///sdcard/1.png"
});
context.startActivity(i);
```

**Note**: Unless an application explicitly exposes an Activity, it is generally not possible to jump to a specific Activity or a specific screen of another app using an intent without root privileges. For example, we can jump to QQ's share screen via Intent because QQ exposes its share Activity publicly. However, without root, we cannot jump to QQ's settings screen via intent because QQ does not expose that Activity.

If you have root privileges, simply add `"root": true` to the intent parameters. For example, to jump to Auto.js settings with root:

```js
app.startActivity({
    packageName: "org.autojs.autojs",
    className: "org.autojs.autojs.ui.settings.SettingsActivity_",
    root: true
});
```

Additionally, regarding how to obtain intent parameters: some intents were discovered accidentally and spread online (for example, jumping to a QQ chat window works because QQ provides a way to jump to customer service QQ via web pages). To obtain parameters of active intents yourself, you can use apps such as "Intent Recorder" or "Implicit Intent Launcher" to intercept internal intents or query exposed ones. Intercepting internal intents typically requires the Xposed framework, or you can obtain parameters through decompilation. In short, there is no simple and direct method.

For more information, search for [Android Intent](https://www.baidu.com/s?wd=android%20Intent) or refer to the [Android Guide: Intents and Intent Filters](https://developer.android.com/guide/components/intents-filters.html#Types).

## app.startActivity(options)

* `options` {Object} Options

Constructs an Intent based on the options and starts the Activity.

```js
app.startActivity({
    action: "SEND",
    type: "text/plain",
    data: "file:///sdcard/1.txt"
});
```

## app.sendBroadcast(options)

* `options` {Object} Options

Constructs an Intent based on the options and sends the broadcast.

## app.startService(options)

* `options` {Object} Options

Constructs an Intent based on the options and starts the service.

## app.sendBroadcast(name)

**[Added in v4.1.0]**

* `name` {string} Specific broadcast name. Available values:
  * `inspect_layout_hierarchy` — Layout hierarchy analysis
  * `inspect_layout_bounds` — Layout bounds

Sending a broadcast with one of the above specific names triggers Auto.js layout analysis, which is useful for script debugging. These broadcasts only take effect when sent from within Auto.js; they have no effect when running in a packaged script.

```js
app.sendBroadcast("inspect_layout_bounds");
```

## app.intentToShell(options)

**[Added in v4.1.0]**

* `options` {Object} Options

Constructs an Intent based on the options and converts it into the corresponding parameters for a shell `am` intent command.

Example:

```js
shell("am start " + app.intentToShell({
    packageName: "org.autojs.autojs",
    className: "org.autojs.autojs.ui.settings.SettingsActivity_"
}), true);
```

See the [Intent specification for the `am` command](https://developer.android.com/studio/command-line/adb#IntentSpec/).

## app.parseUri(uri)

**[Added in v4.1.0]**

* `uri` {string} A string representing a Uri, e.g. `"file:///sdcard/1.txt"`, `"https://www.autojs.org"`
* **returns** {Uri} A Uri object. See [android.net.Uri](https://developer.android.com/reference/android/net/Uri/).

Parses a Uri string and returns the corresponding Uri object. Even if the Uri format is invalid, the function will still return a Uri object. However, accessing its `scheme`, `path`, etc. afterward may return `null` due to parse failure.

**Note**: On newer versions of Android, due to system restrictions that prevent exposing absolute file paths directly in Uris, if the input string is a `file://...` path, the returned Uri will be in the form `content://...`.

## app.getUriForFile(path)

**[Added in v4.1.0]**

* `path` {string} File path, e.g. `"/sdcard/1.txt"`
* **returns** {Uri} A Uri object pointing to the file. See [android.net.Uri](https://developer.android.com/reference/android/net/Uri/).

Creates a Uri object from a file path. **Note**: On newer versions of Android, due to system restrictions that prevent exposing absolute file paths directly in Uris, the returned Uri will be in the form `content://...`.

## app.getInstalledApps([options])

**[[Pro 8.0.0+](https://pro.autojs.org/)]**

* `options` {Object} Options, including:
  * `get`: Specifies what information to include in the returned application data
    * `"activities"` — Activity components of the application
    * `"configurations"` — Hardware configuration of the application
    * `"gids"` — Group IDs of the application
    * `"instrumentation"` — Instrumentation information
    * `"intent_filters"` — Intent filters
    * `"meta_data"` — Meta-data (default)
    * `"permissions"` — Permission information
    * `"providers"` — ContentProvider components
    * `"receivers"` — BroadcastReceiver components
    * `"services"` — Service components
    * `"shared_library_files"` — Shared library files
    * `"signatures"` — Signature information (deprecated)
    * `"signing_certificates"` — Signing certificate information
    * `"uri_permission_patterns"`
    * `"disabled_components"` — Components that have been disabled
    * `"disabled_until_used_components"` — Components disabled until used
    * `"uninstalled_packages"` — Uninstalled packages that still have data
  * `match`: Filters which applications to return
    * `"uninstalled_packages"` — Uninstalled packages that still have data
    * `"disabled_components"` — Disabled components
    * `"disabled_until_used_components"` — Components disabled until used
    * `"system_only"` — System applications only
    * `"factory_only"` — Pre-installed applications only
    * `"apex"` — APEX applications
* **returns** {Array<ApplicationInfo>}

Returns a list of all application packages installed for the current user. If the `match` option `uninstalled_packages` is set, it also includes applications that have been uninstalled but still have data remaining.

The return value is an array of `ApplicationInfo` objects. Returns an empty array if no applications are installed.

The `match` option in `options` is used to specify which applications to return, while the `get` option specifies what information each returned application should carry.

```js
let apps = $app.getInstalledApps({
    // ...
});
```
