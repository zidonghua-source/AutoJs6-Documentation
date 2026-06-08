# Device

---

<p style="font: italic 1em sans-serif; color: #78909C">This chapter is pending supplementation or improvement...</p>
<p style="font: italic 1em sans-serif; color: #78909C">Marked by SuperMonster003 on Oct 22, 2022.</p>

---

The `device` module provides information and operations related to the device, such as getting screen dimensions, memory usage, IMEI, adjusting screen brightness, volume, etc.

Some functions in this module (for example, adjusting volume) require the "Modify system settings" permission. If the permission is not granted, a `SecurityException` will be thrown and the user will be redirected to the permission settings screen.

## device.width

* {number}

Width of the device screen resolution, for example 1080.

## device.height

* {number}

Height of the device screen resolution, for example 1920.

## device.buildId

* {string}

Either a changelist number, or a label like "M4-rc20".

Build ID or revision identifier.

## device.broad

* {string}

The name of the underlying board (e.g. "goldfish").

Board model of the device.

## device.brand

* {string}

The consumer-visible brand associated with the product/hardware (e.g. "Xiaomi", "Huawei").

## device.device

* {string}

The name of the industrial design.

Name of the device in industrial design.

## device.model

* {string}

The end-user-visible name for the end product.

Device model.

## device.product

* {string}

The name of the overall product.

Name of the overall product.

## device.bootloader

* {string}

The system bootloader version number.

Bootloader version of the device.

## device.hardware

* {string}

The name of the hardware (from the kernel command line or /proc).

Hardware name of the device (from kernel command line or /proc).

## device.fingerprint

* {string}

A string that uniquely identifies this build. Do not attempt to parse this value.

Unique identifier of the build.

## device.serial

* {string}

A hardware serial number, if available. Alphanumeric only, case-insensitive.

Hardware serial number.

## device.sdkInt

* {number}

The user-visible SDK version of the framework; its possible values are defined in Build.VERSION_CODES.

Android API level. For example, Android 4.4 has sdkInt = 19.

## device.incremental

* {string}

The internal value used by the underlying source control to represent this build. E.g., a perforce changelist number or a git hash.

## device.release

* {string}

The user-visible version string. E.g., "1.0" or "3.4b5".

Android version number. For example "5.0", "7.1.1".

## device.baseOS

* {string}

The base OS build the product is based on.

## device.securityPatch

* {string}

The user-visible security patch level.

Security patch level.

## device.codename

* {string}

The current development codename, or the string "REL" if this is a release build.

Development codename (e.g. "REL" for release builds).

## device.getIMEI()

* {string}

Returns the device's IMEI.

## device.getAndroidId()

* {string}

Returns the device's Android ID.

Android ID is a 64-bit integer represented as a hexadecimal string. It is randomly generated the first time the device is used and does not change afterward unless the device is factory reset.

## device.getMacAddress()

* {string}

Returns the device's MAC address. This function requires an active WLAN connection to retrieve it; otherwise, it returns null.

**Possible future change**: In the future, root privileges may be used to retrieve the correct MAC address even without a WLAN connection. Therefore, do not rely on this function to determine WLAN connectivity.

## device.getBrightness()

* {number}

Returns the current (manual) brightness. Range is 0~255.

## device.getBrightnessMode()

* {number}

Returns the current brightness mode: 0 for manual brightness, 1 for automatic brightness.

## device.setBrightness(b)

* `b` {number} Brightness, range 0~255

Sets the current manual brightness. If the current mode is automatic brightness, this function will not affect the screen brightness.

This function requires the "Modify system settings" permission. If the permission is not granted, a `SecurityException` will be thrown and the user will be redirected to the permission settings screen.

## device.setBrightnessMode(mode)

* `mode` {number} Brightness mode: 0 for manual, 1 for automatic

Sets the current brightness mode.

This function requires the "Modify system settings" permission. If the permission is not granted, a `SecurityException` will be thrown and the user will be redirected to the permission settings screen.

## device.getMusicVolume()

* {number} Integer value

Returns the current media volume.

## device.getNotificationVolume()

* {number} Integer value

Returns the current notification volume.

## device.getAlarmVolume()

* {number} Integer value

Returns the current alarm volume.

## device.getMusicMaxVolume()

* {number} Integer value

Returns the maximum media volume.

## device.getNotificationMaxVolume()

* {number} Integer value

Returns the maximum notification volume.

## device.getAlarmMaxVolume()

* {number} Integer value

Returns the maximum alarm volume.

## device.setMusicVolume(volume)

* `volume` {number} Volume

Sets the current media volume.

This function requires the "Modify system settings" permission. If the permission is not granted, a `SecurityException` will be thrown and the user will be redirected to the permission settings screen.

## device.setNotificationVolume(volume)

* `volume` {number} Volume

Sets the current notification volume.

This function requires the "Modify system settings" permission. If the permission is not granted, a `SecurityException` will be thrown and the user will be redirected to the permission settings screen.

## device.setAlarmVolume(volume)

* `volume` {number} Volume

Sets the current alarm volume.

This function requires the "Modify system settings" permission. If the permission is not granted, a `SecurityException` will be thrown and the user will be redirected to the permission settings screen.

## device.getBattery()

* {number} Float between 0.0 and 100.0

Returns the current battery percentage.

## device.isCharging()

* {boolean}

Returns whether the device is currently charging.

## device.getTotalMem()

* {number}

Returns the total device memory in bytes (B). 1MB = 1024 * 1024B.

## device.getAvailMem()

* {number}

Returns the currently available memory in bytes (B).

## device.isScreenOn()

* Returns {boolean}

Returns whether the device screen is on. Returns `true` if the screen is on; otherwise returns `false`.

Note: On devices like the vivo Xplay series, the always-on clock when the screen is off does not count as "screen on". Although the screen is technically on, it only displays the clock and is not interactive. In this case, `isScreenOn()` will also return `false`.

## device.wakeUp()

Wakes up the device, including waking up the CPU, screen, etc. Can be used to turn on the screen.

## device.wakeUpIfNeeded()

Wakes up the device if the screen is not on.

## device.keepScreenOn([timeout])

* `timeout` {number} Duration to keep the screen on, in milliseconds. If not specified, the screen stays on indefinitely.

Keeps the screen on.

This function cannot prevent the user from turning off the screen using the lock screen button or similar. It only keeps the screen on when there is no user interaction. Additionally, if the screen is off when this function is called, it will wake the screen.

On some devices, without the `timeout` parameter, the screen may only stay on within the Auto.js interface and will automatically turn off in other interfaces due to the device's power-saving policy. Therefore, it is recommended to use a long duration instead of "keep screen on indefinitely", for example `device.keepScreenOn(3600 * 1000)`.

You can use `device.cancelKeepingAwake()` to cancel the screen-on state.

```js
// Keep screen on indefinitely
device.keepScreenOn()
```

## device.keepScreenDim([timeout])

* `timeout` {number} Duration to keep the screen on, in milliseconds. If not specified, the screen stays on indefinitely.

Keeps the screen on but allows it to dim to save power. This function can be used for scheduled scripts that need to wake the screen without requiring the user to watch it, allowing the screen to dim to save battery.

This function cannot prevent the user from turning off the screen using the lock screen button. It only keeps the screen on when there is no user interaction. If the screen is off when called, it will wake the screen.

You can use `device.cancelKeepingAwake()` to cancel the screen-on state.

## device.cancelKeepingAwake()

Cancels the device's keep-awake state. Used to cancel screen-on states set by functions like `device.keepScreenOn()` and `device.keepScreenDim()`.

## device.vibrate(millis)

* `millis` {number} Vibration duration in milliseconds

Makes the device vibrate for a period of time.

```js
// Vibrate for two seconds
device.vibrate(2000);
```

## device.cancelVibration()

If the device is currently vibrating, this cancels the vibration.
