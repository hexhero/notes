# WSA - Windows安卓子系统

## 安装 WSA

一：进入设置 → 应用 → 可选功能 → 更多 Windows 功能，找到并勾选开启「Hyper-V」和「虚拟机平台」两个选项，安装完成后会提示重启系统。

二：
1. 打开 https://store.rg-adguard.net 
2. 输入 https://www.microsoft.com/store/productid/9p3395vx91nr 选择 Slow，点击对勾
3. 最下方找到文件：MicrosoftCorporationII.WindowsSubsystemForAndroid_1.7.32815.0_neutral___8wekyb3d8bbwe，然后开始下载。
4. 管理员运行 powershell 输入以下命令

```ps
# 安装命令如下：
Add-AppxPackage 安装包路径
```

5. 在 Windows 开始菜单中找到并打开 Windows Subsystem for Android
6. 打开开发者模式
7. 下载ADB调试工具 https://dl.google.com/android/repository/platform-tools_r33.0.1-windows.zip

``` ps
# 第 0 步：确保已正确将 adb 命令加入到系统的环境变量
# 执行下面的命令能看到 adb 版本号则表示 ok
# 如有错误，请检查环境变量是否配置正确
adb version

# 第 1 步：连接 WSA
adb connect 127.0.0.1:58526
# 其中 127.0.0.1:58526 是刚才在 WSA 设置项中看到的 IP

# 第 2 步：安装 APK
# 连接成功之后，就能用下面命令来安装 APK 了
adb install 你的APK文件完整路径
# 注意 .apk 的路径最好无中文且无空格，否则需要用英文双引号包裹。
# 安装完成后，在 Windows 开始菜单的“所有应用”里就能找到你安装的 Android 应用
```

这样就能使用 adb 命令安装 apk 文件到 Windows 11 安卓子系统 WSA 了。重点是开启开发者模式，获得正确 IP 地址以及正确安装 adb 命令。


参考:
* https://zhuanlan.zhihu.com/p/424959704

## 配置 Finder 抓包

1. 打开设置页面
```sh
adb shell am start -n com.android.settings/com.android.settings.Settings
```
2. 设置Finder代理，ip 与 网关一致.
3. 在设置页面配置证书.