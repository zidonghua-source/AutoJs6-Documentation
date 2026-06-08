# Shell

---

<p style="font: italic 1em sans-serif; color: #78909C">This section is to be supplemented or improved...</p>
<p style="font: italic 1em sans-serif; color: #78909C">Marked by SuperMonster003 on Oct 22, 2022.</p>

---

Shell refers to Unix Shell, which provides a series of commands for interacting with the operating system on Unix-like systems.

Many programs can be used to execute shell commands, such as terminal emulators.

In Auto.js, it is roughly equivalent to executing the command "adb shell" via adb. There are two implementation methods:

* Execution via `java.lang.Runtime.exec` (functions such as shell, Tap, Home, etc.)
* Execution via the built-in terminal emulator (RootAutomator, Shell objects, etc.)

# shell function

## shell(cmd[, root])

* cmd {string} The command to execute
* root {Boolean} Whether to run with root privileges, default is false.

Executes the command cmd once and returns the execution result. The returned object has the following properties:

* code {number} Return code. 0 on success, non-zero on failure.
* result {string} Execution result (stdout output)
* error {string} Error information from execution (stderr output). For example, if a command requiring root privileges is executed without granting root access, it returns the error "Permission denied".

Example (force stop WeChat):

```
var result = shell("am force-stop com.tencent.mm", true);
log(result);
console.show();
if(result.code == 0){
  toast("Execution succeeded");
}else{
  toast("Execution failed! Please check the error information in the console");
}
```

# Shell

The shell function is used to execute a single command once and obtain the result. If multiple commands need to be executed, using a Shell object is more efficient. This is because each call to the shell function opens a separate shell process and closes it after execution, which takes some time; whereas the Shell object uses the same shell process from start to finish.

## new Shell(root)

* root {Boolean} Whether to run a shell process with root privileges, default is false. This will affect the privileges of commands executed later using this Shell object.

The "constructor" of the Shell object.

```
var sh = new Shell(true);
// Force stop WeChat
sh.exec("am force-stop com.tencent.mm");
sh.exit();
```

## Shell.exec(cmd)

* `cmd` {string} The command to execute

Executes the command cmd. This function does not return any value.

Note that command execution is "asynchronous" and non-blocking. That is, it will not wait for the command to complete before continuing to the next line.

Although this design is somewhat inconvenient to use, it is limited by the terminal emulator and there is currently no solution. If a solution is found in the future, a `Shell.execAndWaitFor` function will be provided.

## Shell.exit()

Exits the shell directly. Any currently executing command will be forcibly terminated.

## Shell.exitAndWaitFor()

Executes the "exit" command and waits for the command to finish executing and for the shell to exit.

This function executes the exit command to exit the shell normally.

## Shell.setCallback(callback)

* callback {Object} Callback function

Sets the callback function for this Shell to monitor the Shell's output. It can include the following properties:

* onOutput {Function} Called whenever the shell has new output. Its parameter is a string.
* onNewLine {Function} Called whenever the shell has a new line of output. Its parameter is a string (without the trailing newline).

Example:

```
var sh = new Shell();
sh.setCallback({
	onNewLine: function(line){
		// Print new lines of output to the console
		log(line);
	}
})
while(true){
	// Loop to input commands
	var cmd = dialogs.rawInput("Please enter the command to execute, type exit to quit");
	if(cmd == "exit"){
		break;
	}
	// Execute command
	sh.exec(cmd);
}
sh.exit();
```

# Appendix: Brief Introduction to Shell Commands

The following information about shell commands comes from the [Android Studio User Guide: Shell Commands](https://developer.android.com/studio/command-line/adb.html#shellcommands/).

## am command

The am command is the Activity Manager command, used to manage application activities, services, etc.

**All the following commands start with "am ", for example `shell('am start -p com.tencent.mm');` (launch WeChat)**

### start [options] intent

Starts the Activity (application activity) specified by the intent.   
See [Intent parameter specification](#shell_intent).

Options include:

* -D: Enable debugging.
* -W: Wait for the launch to complete.
* --start-profiler file: Start the profiler and send results to file.
* -P file: Similar to --start-profiler, but profiling stops when the app becomes idle.
* -R count: Repeat Activity launch count times. Before each repetition, finish the top Activity.
* -S: Force stop the target app before starting the Activity.
* --opengl-trace: Enable OpenGL function tracing.
* --user user_id | current: Specify which user to run as; if not specified, run as the current user.

### startservice [options] intent

Starts the Service specified by the intent.   
See [Intent parameter specification](#shell_intent).   
Options include:

* --user user_id | current: Specify which user to run as; if not specified, run as the current user.

### force-stop package

Force stops all applications associated with the package ([application package name](#application-package-name)).

### kill [options] package

Terminates all processes associated with the package ([application package name](#application-package-name)). This command only terminates processes that can be safely terminated without affecting the user experience.   
Options include:

* --user user_id | all | current: Specify the user whose processes will be terminated; if not specified, terminate processes for all users.

### kill-all

Terminates all background processes.

### broadcast [options] intent

Sends a broadcast intent.
See [Intent parameter specification](#shell_intent).

Options include:

* [--user user_id | all | current]: Specify the user to send to; if not specified, send to all users.

### instrument [options] component

Start monitoring using an Instrumentation instance. Typically, the target component is of the form test_package/runner_class.   
Options include:

* -r: Output raw results (otherwise decode report_key_streamresult). Use with [-e perf true] to generate raw output for performance measurements.
* -e name value: Set the parameter name to value. For test runners, the general form is -e testrunner_flag value[,value...].
* -p file: Write profiling data to file.
* -w: Wait for instrumentation to complete before returning. Test runners must use this option.
* --no-window-animation: Disable window animations at runtime.
* --user user_id | current: Specify the user in which the instrumentation runs; if not specified, run in the current user.
* profile start process file: Start the profiler for process and write results to file.
* profile stop process: Stop the profiler for process.

### dumpheap [options] process file

Dump the heap of process and write it to file.

Options include:

* --user [user_id|current]: When a process name is provided, specify the user of the process to dump; if not specified, use the current user.
* -n: Dump the native heap instead of the managed heap.
* set-debug-app [options] package: Set the application package as debuggable.

Options include:

* -w: Wait for the debugger when the app starts.
* --persistent: Retain this value.
* clear-debug-app: Use set-debug-app to clear previously set packages for debugging purposes.

### monitor [options]

Start monitoring for crashes or ANRs.

Options include:

* --gdb: Start gdbserv on the given port during crash/ANR.

### screen-compat {on|off} package

Control the screen compatibility mode of package.

### display-size [reset|widthxheight]

Override the emulator/device display size. This command is very useful for testing your app on screens of different sizes; it supports using a large-screen device to emulate small-screen resolution (and vice versa).   
Example:

```
shell("am display-size 1280x800", true);
	
```

### display-density dpi

Override the emulator/device display density. This command is very useful for testing your app on screens of different densities; it supports using a low-density screen to test in a high-density environment (and vice versa).   
Example:

```
shell("am display-density 480", true);
```

### to-uri intent

Output the given intent specification in URI form.
See [Intent parameter specification](#shell_intent).

### to-intent-uri intent

Output the given intent specification in intent:URI form.
See the intent parameter specification.

### Intent parameter specification

For am commands that use intent parameters, you can use the following options to specify the intent:

* -a action  
  Specify the intent action, such as “android.intent.action.VIEW”. This can be declared only once.
* -d data_uri  
  Specify the intent data URI, such as “content://contacts/people/1”. This can be declared only once.
* -t mime_type  
  Specify the intent MIME type, such as “image/png”. This can be declared only once.
* -c category  
  Specify the intent category, such as “android.intent.category.APP_CONTACTS”.
* -n component  
  Specify the component name with package name prefix to create an explicit intent, such as “com.example.app/.ExampleActivity”.
* -f flags  
  Add flags to the intent supported by setFlags().
* --esn extra_key  
  Add a null extra. Not supported for URI intents.
* -e|--es extra_key extra_string_value  
  Add string data as a key-value pair.
* --ez extra_key extra_boolean_value  
  Add boolean data as a key-value pair.
* --ei extra_key extra_int_value  
  Add integer data as a key-value pair.
* --el extra_key extra_long_value  
  Add long integer data as a key-value pair.
* --ef extra_key extra_float_value  
  Add float data as a key-value pair.
* --eu extra_key extra_uri_value  
  Add URI data as a key-value pair.
* --ecn extra_key extra_component_name_value  
  Add component name, converted and passed as a ComponentName object.
* --eia extra_key extra_int_value[,extra_int_value...]  
  Add integer array.
* --ela extra_key extra_long_value[,extra_long_value...]  
  Add long integer array.
* --efa extra_key extra_float_value[,extra_float_value...]  
  Add float array.
* --grant-read-uri-permission  
  Include the FLAG_GRANT_READ_URI_PERMISSION flag.
* --grant-write-uri-permission  
  Include the FLAG_GRANT_WRITE_URI_PERMISSION flag.
* --debug-log-resolution  
  Include the FLAG_DEBUG_LOG_RESOLUTION flag.
* --exclude-stopped-packages  
  Include the FLAG_EXCLUDE_STOPPED_PACKAGES flag.
* --include-stopped-packages  
  Include the FLAG_INCLUDE_STOPPED_PACKAGES flag.
* --activity-brought-to-front  
  Include the FLAG_ACTIVITY_BROUGHT_TO_FRONT flag.
* --activity-clear-top  
  Include the FLAG_ACTIVITY_CLEAR_TOP flag.
* --activity-clear-when-task-reset  
  Include the FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET flag.
* --activity-exclude-from-recents  
  Include the FLAG_ACTIVITY_EXCLUDE_FROM_RECENTS flag.
* --activity-launched-from-history  
  Include the FLAG_ACTIVITY_LAUNCHED_FROM_HISTORY flag.
* --activity-multiple-task  
  包含标志 FLAG_ACTIVITY_MULTIPLE_TASK.
* --activity-no-animation  
  包含标志 FLAG_ACTIVITY_NO_ANIMATION.
* --activity-no-history  
  包含标志 FLAG_ACTIVITY_NO_HISTORY.
* --activity-no-user-action  
  包含标志 FLAG_ACTIVITY_NO_USER_ACTION.
* --activity-previous-is-top  
  包含标志 FLAG_ACTIVITY_PREVIOUS_IS_TOP.
* --activity-reorder-to-front  
  包含标志 FLAG_ACTIVITY_REORDER_TO_FRONT.
* --activity-reset-task-if-needed  
  包含标志 FLAG_ACTIVITY_RESET_TASK_IF_NEEDED.
* --activity-single-top  
  包含标志 FLAG_ACTIVITY_SINGLE_TOP.
* --activity-clear-task  
  包含标志 FLAG_ACTIVITY_CLEAR_TASK.
* --activity-task-on-home  
  包含标志 FLAG_ACTIVITY_TASK_ON_HOME.
* --receiver-registered-only  
  包含标志 FLAG_RECEIVER_REGISTERED_ONLY.
* --receiver-replace-pending  
  包含标志 FLAG_RECEIVER_REPLACE_PENDING.
* --selector  
  需要使用 -d 和 -t 选项以设置 intent 数据和类型.

#### URI component package

如果不受上述某一选项的限制, 您可以直接指定 URI、软件包名称和组件名称. 当参数不受限制时, 如果参数包含一个“:”（冒号）, 则此工具假定参数是一个 URI；如果参数包含一个“/”（正斜杠）, 则此工具假定参数是一个组件名称；否则, 此工具假定参数是一个软件包名称.

## 应用包名

所谓应用包名, 是唯一确定应用的标识. 例如微信的包名是"com.tencent.mm", QQ的包名是"com.tencent.mobileqq".   
要获取一个应用的包名, 可以通过函数`getPackageName(appName)`获取. 参见帮助->其他一般函数.

## pm命令

pm命令用于管理应用程序, 例如卸载应用、冻结应用等.   
**以下命令均以"pm "开头, 例如"shell(\"pm disable com.tencent.mm\");"(冻结微信)**

### list packages [options] filter

输出所有软件包, 或者, 仅输出包名称包含 filter 中的文本的软件包.   
选项：

* -f：查看它们的关联文件.
* -d：进行过滤以仅显示已停用的软件包.
* -e：进行过滤以仅显示已启用的软件包.
* -s：进行过滤以仅显示系统软件包.
* -3：进行过滤以仅显示第三方软件包.
* -i：查看软件包的安装程序.
* -u：也包括卸载的软件包.
* --user user_id：要查询的用户空间.

### list permission-groups

输出所有已知的权限组.

### list permissions [options] group

输出所有已知权限, 或者, 仅输出 group 中的权限.   
选项：

* -g：按组加以组织.
* -f：输出所有信息.
* -s：简短摘要.
* -d：仅列出危险权限.
* -u：仅列出用户将看到的权限.

### list instrumentation [options]

列出所有测试软件包.   
选项：

* -f：列出用于测试软件包的 APK 文件.
* target_package：列出仅用于此应用的测试软件包.

### list features

输出系统的所有功能.

### list libraries

输出当前设备支持的所有库.

### list users

输出系统上的所有用户.

### path package

输出给定 package 的 APK 的路径.

### install [options] path

将软件包（通过 path 指定）安装到系统.   
选项：

* -l：安装具有转发锁定功能的软件包.
* -r：重新安装现有应用, 保留其数据.
* -t：允许安装测试 APK.
* -i installer_package_name：指定安装程序软件包名称.
* -s：在共享的大容量存储（如 sdcard）上安装软件包.
* -f：在内部系统内存上安装软件包.
* -d：允许版本代码降级.
* -g：授予应用清单文件中列出的所有权限.

### uninstall [options] package

从系统中卸载软件包.   
选项：

* -k：移除软件包后保留数据和缓存目录.

### clear package

删除与软件包关联的所有数据.

### enable package_or_component

启用给定软件包或组件（作为“package/class”写入）.

### disable package_or_component

停用给定软件包或组件（作为“package/class”写入）.

### disable-user [options] package_or_component

选项：

* --user user_id：要停用的用户.

### grant package_name permission

向应用授予权限. 在运行 Android 6.0（API 级别 23）及更高版本的设备上, 可以是应用清单中声明的任何权限. 在运行 Android 5.1（API 级别 22）和更低版本的设备上, 必须是应用定义的可选权限.

### revoke package_name permission

从应用中撤销权限. 在运行 Android 6.0（API 级别 23）及更高版本的设备上, 可以是应用清单中声明的任何权限. 在运行 Android 5.1（API 级别 22）和更低版本的设备上, 必须是应用定义的可选权限.

### set-install-location location

更改默认安装位置. 位置值：

* 0：自动—让系统决定最佳位置.
* 1：内部—安装在内部设备存储上.
* 2：外部—安装在外部介质上.

> 注：此命令仅用于调试目的；使用此命令会导致应用中断和其他意外行为.

### get-install-location

返回当前安装位置. 返回值：

* 0 [auto]：让系统决定最佳位置.
* 1 [internal]：安装在内部设备存储上
* 2 [external]：安装在外部介质上

### set-permission-enforced permission [true|false]

指定是否应强制执行给定的权限.

### trim-caches desired_free_space

减少缓存文件以达到给定的可用空间.

### create-user user_name

使用给定的 user_name 创建新用户, 输出新用户的标识符.

### remove-user user_id

移除具有给定的 user_id 的用户, 删除与该用户关联的所有数据.

### get-max-users

输出设备支持的最大用户数.

## 其他命令

### 进行屏幕截图

screencap 命令是一个用于对设备显示屏进行屏幕截图的 shell 实用程序. 在 shell 中, 此语法为：

```
screencap filename
```

例如：

```
$ shell("screencap /sdcard/screen.png");
```

### 列表文件

```
ls filepath
```

例如:

```
log(shell("ls /system/bin").result);
```
