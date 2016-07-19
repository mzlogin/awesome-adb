# awesome-adb

Adb 用法大全。

## 目录

* [查看手机型号](#查看手机型号)
* [查看手机电池状况](#查看手机电池状况)
* [查看手机分辨率](#查看手机分辨率)
* [查看 android\_id](#查看-android_id)
* [录制屏幕](#录制屏幕)
* [查看前台 Activity](#查看前台-activity)

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
