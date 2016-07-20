# Adb 用法大全

Adb，即 [Android Debug Bridge](https://developer.android.com/studio/command-line/adb.html)，它是 Android 开发/测试人员不可替代的强大工具，也是 Android 手机玩家的好玩具。

## 目录

* [设备连接管理](#设备连接管理)
	* [查询已连接设备/模拟器](#查询已连接设备模拟器)
	* [无线连接](#无线连接)
* [应用管理](#应用管理)
	* [查看所有已安装应用](#查看所有已安装应用)
	* [安装 APK](#安装-apk)
	* [卸载应用](#卸载应用)
	* [调起应用](#调起应用)
	* [查看前台 Activity](#查看前台-activity)
* [调试](#调试)
	* [查看/过滤日志](#查看过滤日志)
* [查看设备信息](#查看设备信息)
	* [查看手机型号](#查看手机型号)
	* [查看手机电池状况](#查看手机电池状况)
	* [查看手机分辨率](#查看手机分辨率)
	* [查看 android\_id](#查看-android_id)
* [其它实用功能](#其它实用功能)
	* [录制屏幕](#录制屏幕)
* [参考链接](#参考链接)

## 设备连接管理

### 查询已连接设备/模拟器

命令：

```
adb devices
```

输出示例：

```
List of devices attached
cf264b8f	device
emulator-5554	device
```

该输出显示当前已经连接了两台设备/模拟器，`cf264b8f` 与 `emulator-5554` 分别是它们的 SN。从 `emulator-5554` 这个名字可以看出它是一个 Android 模拟器。

常见异常输出：

1. 没有设备/模拟器连接成功。

   ```
   List of devices attached
   ```

2. 设备/模拟器未连接到 adb 或它无法响应。

   ```
   List of devices attached
   cf264b8f	offline
   ```

### 无线连接

// TODO

## 应用管理

### 查看所有已安装应用

命令：

```
adb shell pm list packages
```

输出示例：

```
package:com.android.smoketest
package:com.example.android.livecubes
package:com.android.providers.telephony
package:com.google.android.googlequicksearchbox
package:com.android.providers.calendar
package:com.android.providers.media
package:com.android.protips
package:com.android.documentsui
package:com.android.gallery
package:com.android.externalstorage
...
// other packages here
...
```

### 安装 APK

命令：

```
adb install /path/to/filename.apk
```

参数：

`adb install` 后面可以跟一些参数来控制安装 APK 的行为，常用参数及含义如下：

| 参数 | 含义                  |
|------|-----------------------|
| -r   | 允许覆盖安装。        |
| -s   | 将应用安装到 sdcard。 |
| -d   | 允许降级覆盖安装。    |

完整参数列表及含义可以直接运行 `adb` 命令然后查看 `adb install [-lrtsdg] <file>` 一节。

如果见到类似如下输出（状态为 `Success`）代表安装成功：

```
12040 KB/s (22205609 bytes in 1.801s)
        pkg: /data/local/tmp/SogouInput_android_v8.3_sweb.apk
Success
```

而如果状态为 `Failure` 则表示安装失败。常见安装失败输出代码、含义及可能的解决办法如下：

| 输出                                               | 含义                                             | 解决办法                     |
|----------------------------------------------------|--------------------------------------------------|------------------------------|
| INSTALL\_FAILED\_ALREADY\_EXISTS                   | 应用已经存在                                     | 使用 `-r` 参数               |
| INSTALL\_FAILED\_OLDER\_SDK                        | 设备系统版本低于应用要求                         | 使用高版本 Android 系统      |
| INSTALL\_FAILED\_INSUFFICIENT\_STORAGE             | 空间不足                                         | 清理空间                     |
| INSTALL\_FAILED\_MEDIA\_UNAVAILABLE                | 安装位置不可用                                   |                              |
| INSTALL\_FAILED\_VERSION\_DOWNGRADE                | 已经安装了更高版本                               | 使用 `-d` 参数               |
| INSTALL\_CANCELED\_BY\_USER                        | 应用安装需要在设备上确认，但未操作设备或点了取消 | 在设备上同意安装             |
| INSTALL\_PARSE\_FAILED\_INCONSISTENT\_CERTIFICATES | 已安装该应用，且签名与 APK 文件不一致            | 先卸载手机上的该应用，再安装 |
| INSTALL\_FAILED\_INVALID\_URI                      | 无效的 APK 文件名                                | 确保 APK 文件名里无中文    |
| Offline                                            | 设备未连接成功                                   | 先将设备与 adb 连接成功      |
| error: device not found                            | 没有连接成功的设备                               | 先将设备与 adb 连接成功      |
| protocol failure                                   | 设备已断开连接                                   | 先将设备与 adb 连接成功      |
| Unknown option: -s                                 | Android 2.2 以下不支持安装到 sdcard              | 不使用 `-s` 参数             |

### 卸载应用

// TODO

### 调起应用

// TODO

### 查看前台 Activity

命令：

```
adb shell dumpsys activity activities | grep mFocusedActivity
```

输出示例：

```
mFocusedActivity: ActivityRecord{8079d7e u0 com.cyanogenmod.trebuchet/com.android.launcher3.Launcher t42}
```

其中的 `com.cyanogenmod.trebuchet/com.android.launcher3.Launcher` 就是当前处于前台的 Activity。

## 调试

### 查看/过滤日志

// TODO

## 查看设备信息

### 查看手机型号

命令：

```
adb shell getprop ro.product.model
```

输出示例：

```
Nexus 5
```

### 查看手机电池状况

命令：

```
adb shell dumpsys battery
```

输入示例：

```
Current Battery Service state:
  AC powered: false
  USB powered: true
  Wireless powered: false
  status: 2
  health: 2
  present: true
  level: 44
  scale: 100
  voltage: 3872
  temperature: 280
  technology: Li-poly
```

其中 `scale` 代表最大电量，`level` 代表当前电量。上面的输出表示还剩下 44% 的电量。

### 查看手机分辨率

命令：

```
adb shell dumpsys window displays
```

输出示例：

```
WINDOW MANAGER DISPLAY CONTENTS (dumpsys window displays)
  Display: mDisplayId=0
    init=1080x1920 480dpi cur=1080x1920 app=1080x1776 rng=1080x1005-1794x1701
    deferred=false layoutNeeded=false
    ...
    // some other output here
    ...
```

### 查看 android\_id

命令：

```
adb shell settings get secure android_id
```

输出示例：

```
51b6be48bac8c569
```

## 其它实用功能

### 录制屏幕

录制屏幕以 mp4 格式保存到 /sdcard：

```
adb shell screenrecord /sdcard/filename.mp4
```

需要停止时按 <kbd>Ctrl-C</kbd>，默认录制时间和最长录制时间都是 180 秒。

如果需要导出到电脑：

```
adb pull /sdcard/filename.mp4
```

`screenrecord` 命令也支持一些参数，可以使用 `adb shell screenrecord --help` 查看，下面是简介：

| 参数                | 含义                                            |
|---------------------|-------------------------------------------------|
| --size WIDTHxHEIGHT | 视频的尺寸，比如 `1280x720`，默认是屏幕分辨率。 |
| --bit-rate RATE     | 视频的比特率，默认是 4Mbps。                    |
| --time-limit TIME   | 录制时长，单位秒。                              |
| --verbose           | 输出更多信息。                                  |

## 参考链接

* [Android Debug Bridge](https://developer.android.com/studio/command-line/adb.html)
* [ADB Shell Commands](https://developer.android.com/studio/command-line/shell.html)
