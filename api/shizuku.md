# Shizuku

---

<p style="font: italic 1em sans-serif; color: #78909C">This chapter is pending supplementation or improvement...</p>
<p style="font: italic 1em sans-serif; color: #78909C">Marked by SuperMonster003 on Oct 30, 2023.</p>

---

Through [Shizuku](https://shizuku.rikka.app/introduction/) you can obtain ADB privileges and use system APIs.

To use Shizuku, all of the following conditions must be met:

- The [Shizuku app](https://github.com/RikkaApps/Shizuku/releases) is installed on the device (version `11` or higher)
- The Shizuku service is running (see the [Shizuku User Guide](https://shizuku.rikka.app/guide/setup/#start-shizuku))
- The Shizuku permission switch is enabled in the AutoJs6 home screen drawer

---

<p style="font: bold 2em sans-serif; color: #FF7043">shizuku</p>

---

## [@] shizuku

`shizuku` can be used as a global object:

```js
typeof shizuku; // "function"
typeof shizuku.execCommand; // "function"
```

### shizuku(cmd)

**`6.4.0`** **`Overload 1/2`**

- **cmd** { [string](dataTypes#string) } - Command to execute
- <ins>**returns**</ins> { [ShellResult](shellResultType) } - Shell result

Executes a command using Shizuku.

```js
/* Simulate the back key. */
shizuku('input keyevent 4');
shizuku(`input keyevent ${KeyEvent.KEYCODE_BACK}`); /* Same as above. */

/* Simulate the power key. */
shizuku('input keyevent 26');
shizuku(`input keyevent ${KeyEvent.KEYCODE_POWER}`); /* Same as above. */

/* Tap screen coordinates (100, 120). */
shizuku("input tap 100 120");

/* Grant AutoJs6 the "Modify secure settings" permission. */
shizuku('pm grant org.autojs.autojs6 android.permission.WRITE_SECURE_SETTINGS');

/* Grant AutoJs6 the "Project media" permission. */
shizuku('appops set org.autojs.autojs6 PROJECT_MEDIA allow');

/* Enable the AutoJs6 Accessibility service. */
shizuku('settings put secure enabled_accessibility_services org.autojs.autojs6/org.autojs.autojs.core.accessibility.AccessibilityServiceUsher');

/* Get the current time. */
console.log(shizuku('date').result.trim());
```

### shizuku(cmdList)

**`6.4.0`** **`Overload 2/2`**

- **cmdList** { [string](dataTypes#string)[[]](dataTypes#array) } - List of commands to execute (one per line)
- <ins>**returns**</ins> { [ShellResult](shellResultType) } - Shell result

Executes multiple commands at once using Shizuku. Each element in the `cmdList` array corresponds to one command.

```js
shizuku([ 'cmd-a', 'cmd-b', 'cmd-c' ]);
shizuku('cmd-a\ncmd-b\ncmd-c'); /* Same as above. */
```

[//]: # (```ts)

[//]: # (// class WrappedShizuku {)

[//]: # (//     public static service: org.autojs.autojs.core.shizuku.IUserService;)

[//]: # (//     public hasPermission&#40;&#41;: boolean;)

[//]: # (//     public config&#40;&#41;: android.content.Intent;)

[//]: # (//     public ensureService&#40;&#41;: void;)

[//]: # (//     public config&#40;isRequest: java.lang.Boolean&#41;: android.content.Intent;)

[//]: # (//     public isInstalled&#40;&#41;: boolean;)

[//]: # (//     public requestPermission&#40;&#41;: void;)

[//]: # (//     public execCommand&#40;cmdList: string[]&#41;: org.autojs.autojs.runtime.api.AbstractShell.Result;)

[//]: # (//     public execCommand&#40;cmd: string&#41;: org.autojs.autojs.runtime.api.AbstractShell.Result;)

[//]: # (// })

[//]: # (```)