### 1.查看正在运行的应用进程 ###
方法一：**adb shell ps [startStr]**  --------匹配规则startWiths(startStr)
方法二：**adb shell ps | findstr [containsStr]**  --------匹配规则contains(containsStr)


### 2.安装应用 ###
方法一：**adb push xx.apk** 发送指定的apk到 **/sdcard/test/**目录下
方法二：**adb install xx.apk** 有时候会出现已经安装相同包名的错误，可以用方法三
方法三：**adb install -r xx.apk** 强制安装

### 3.开启/关闭adb ###
开启：**adb start-server**
关闭：**adb kill-server**