# uiautomator 相关命令

dump出当前窗口的UI布局信息，输出的文件可以用 sdk/tools/uiautomatorviewer.bat 工具打开查看。

<!-- vim-markdown-toc GFM -->
* [获取当前页面布局](#获取当前页面布局)
<!-- vim-markdown-toc -->


### 获取当前页面布局
```sh
adb shell uiautomator dump /data/local/tmp/uidump.xml  && adb pull /data/local/tmp/uidump.xml uidump.xml
```
