## 一、adb的构成和工作原理
    1.adb 安卓调试桥 是一个 调试工具
    2.adb 包含 三个部分 
        * Client端：运⾏行行在开发机器器中，即你的开发电脑，⽤用来发送 adb 命令；
        * Daemon 守护进程：运⾏行行在调试设备中，⼿手机或模拟器器，⽤用来接收并执⾏行行 adb 命令；
        * Server端：同样运⾏行行在开发机器器中，⽤用来管理理 Client 端和⼿手机的 Daemon 之间的通信。

## 二、常用命令
    1.获取包名(唯一的)和界面名(应用)
        * window: adb shell dumpsys window | findstr mFocusedApp
        * 包名:   com.android.settings
        * 界面名(启动名): com.coloros.settings.feature.homepage.ColorSettingsHomepageActivity
    
    2.文件传输
        * adb push 电脑路径 手机路径
            adb push "C:\Users\yui\Desktop\source.xml" /sdcard(手机文件夹路径)
        * adb pull 手机 电脑
    
    3.获取app启动时间
        * adb shell am start -w 包名/界面名

    4.获取手机日志
        * adb logcat

    5.其他
        * adb install xxx.apk
        * adb uninstall package
        * adb devices
        * adb shell               进入安卓命令行解释器(类似于* linux shell)
        * adb connect [ip:post]   网络adb
        * adb -s 设备名称 reboot   重启
        * adb shell reboot -p     关机

        * 模拟按键
        * * adb shell input keyevent 3/4/20/26/66/187  #home键/返回键/向下/电源键/回车/多任务键
        * * 模拟输入 (要有输入框)
        * * adb shell input text "hello world"
        * 模拟点击
        * * adb shell input tap x y
        * * adb shell input swipe .....

        * 实现安装包 提取(无需root)
        * * adb shell pm list package   查看 安装的apk 列表
        * * adb shell pm path 包名      查看 相关包的安装路径，即在data/app/...(pwd查看* * 当前所在路径)
        * * adb shell cp /data/appxxx.apk(apk 路径) /sdcard   将apk 文件复制到 /sdcard 路径下

        * 网络adb
        * * 先连接usb手机
        * * adb tcpip 5555      开启 手机端 5555端口(adb默认 5555)，即可 断开连接
        * * adb connect ip:port     port 不写默认 5555，网络adb连接
        * * adb disconnect ip:port  断开连接

        * 网络adb 多台设备    多一个参数 手机设备号
        * * 在连接usb手机
        * * adb -s 设备号 tcpip 5556
        ......

        * adb shell ifconfig | findstr 192                            查看内网 ip
        * adb shell screencap /sdcard/screen.png                      截屏
        * adb shell screenrecord  --time-limit 10 /sdcard/test.mp4    录屏10s(需要root)

        * adb shell am start -n package/launch activity
        * adb shell am start -n com.android.settings/.Settings activity   启动设置程序
        * adb shell am force-stop package                                 关闭程序
        * adb shell am restart                                            重启
        * adb shell service list                                          查看当前运行的服务

        ============ PC键盘===================
        * 切换输入法
        * * adb shell ime list -s                                       查看输入法列表
        * * adb shell ime set com.android.adbkeyboard/.AdbIME           设置输入法

        * 使用 adb keyboard键盘， 解决 adb无法输入中文字符问题
        * 手机 安装 ADBKeyboard.apk 即可
        * adb shell am broadcast -a ADB_INPUT_TEXT --es msg 你好世界

        * 使用 WiFikeyboard（apk）,来控制手机输入
        * 键盘输入模式 选择 "wifi keyboard"
        * usb 连接
        * adb forward tcp:7777 tcp:7777
        * 浏览器 回环地址:7777        即可

        * 使用 Remote keyboard （apk） 
        * 键盘输入模式 选择 "Remote keyboard"
        * 在 PC 端，您需要一个 telnet 客户端来建立连接
        * 如 Putty


        ==========分辨率/dpi==============
        * adb shell wm density (数值)                 查看(/修改)dpi
        * adb shell wm size (宽x高)                   查看(/修改)分辨率   

        =========判断键盘是否打开==========
        * adb shell dumpsys input_method | findstr mInputShown    true/false 



