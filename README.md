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
* [查看设备信息](#查看设备信息)
	* [查看手机型号](#查看手机型号)
	* [查看手机电池状况](#查看手机电池状况)
	* [查看手机分辨率](#查看手机分辨率)
	* [查看 android\_id](#查看-android_id)
* [其它实用功能](#其它实用功能)
	* [录制屏幕](#录制屏幕)

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

### 无线连接

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
package:com.android.htmlviewer
package:com.android.mms.service
package:com.android.providers.downloads
package:com.android.messaging
package:com.android.browser
package:com.android.soundrecorder
package:com.android.defcontainer
package:com.android.providers.downloads.ui
package:com.android.vending
package:com.android.pacprocessor
package:com.wooyun.summit
package:com.android.certinstaller
package:android
package:com.android.contacts
package:com.android.backupconfirm
package:com.google.android.launcher
package:com.android.statementservice
package:com.android.calendar
package:com.android.providers.settings
package:com.android.sharedstoragebackup
package:com.android.printspooler
package:com.android.dreams.basic
package:com.android.webview
package:com.android.inputdevices
package:com.android.backuptester
package:com.android.sdksetup
package:com.google.android.apps.maps
package:com.android.development_settings
package:com.android.server.telecom
package:com.android.keychain
package:com.android.camera
package:com.android.dialer
package:com.android.emulator.smoketests
package:com.google.android.gms
package:com.google.android.gsf
package:com.android.packageinstaller
package:com.svox.pico
package:com.example.android.apis
package:com.android.proxyhandler
package:com.android.fallback
package:com.android.inputmethod.latin
package:com.android.managedprovisioning
package:com.google.android.gsf.login
package:com.android.wallpaper.livepicker
package:com.android.netspeed
package:jp.co.omronsoft.openwnn
package:com.android.settings
package:com.android.calculator2
package:com.android.gesture.builder
package:com.android.vpndialogs
package:com.android.email
package:com.android.music
package:com.android.phone
package:com.android.shell
package:com.android.providers.userdictionary
package:com.android.location.fused
package:com.android.deskclock
package:com.android.systemui
package:com.android.exchange
package:com.android.smoketest.tests
package:com.android.customlocale2
package:com.example.android.softkeyboard
package:org.mazhuang.androiduidemos
package:com.google.android.play.games
package:com.android.development
package:com.android.providers.contacts
package:com.android.captiveportallogin
package:com.android.widgetpreview
```

### 安装 APK

命令：

```
adb install /path/to/filename.apk
```

// TODO: 命令行参数，常见错误输出等

### 卸载应用

### 调起应用

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
|:--------------------|:------------------------------------------------|
| --size WIDTHxHEIGHT | 视频的尺寸，比如 `1280x720`，默认是屏幕分辨率。 |
| --bit-rate RATE     | 视频的比特率，默认是 4Mbps。                    |
| --time-limit TIME   | 录制时长，单位秒。                              |
| --verbose           | 输出更多信息。                                  |
