# dumpsys 相关命令

<!-- vim-markdown-toc GFM -->
* [获取当前Activity](#获取当前activity)
* [获取当前Window](#获取当前window)
<!-- vim-markdown-toc -->


### 获取当前Activity

Linux:
```sh
adb shell dumpsys activity | grep "mFocusedActivity"
```

Windows:
```sh
adb shell dumpsys activity  | findstr "mFocusedActicity"
```

### 获取当前Window

```sh
adb shell dumpsys window w | grep \/  |  grep name=
```

