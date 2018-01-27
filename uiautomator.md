# uiautomator 相关命令

<!-- vim-markdown-toc GFM -->
* [获取当前页面布局](#获取当前页面布局)
<!-- vim-markdown-toc -->


### 获取当前页面布局
```sh
adb shell uiautomator dump /data/local/tmp/uidump.xml  && adb pull /data/local/tmp/uidump.xml uidump.xml
```
