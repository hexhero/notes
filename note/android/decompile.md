# APK 反编译

## APK Tool 

反编译APK

### APK 打包后的需要重新签名

使用java自带的Keytool 为 demo.apk 签名

生成证书

```
keytool -genkey -keystore my-release-key.keystore -alias my_alias -keyalg RSA -keysize 4096 -validity 10000
```

用证书给 apk 签名

```
jarsigner -sigalg MD5withRSA -digestalg SHA1 -keystore my-release-key.keystore -signedjar sign_demo.apk demo.apk my_alias
```

sign_demo.apk 就有签名了。

## dex2jar 或者 enjarfy

将APK反编译jar包

## jd-gui

反编译 jar 包，查看 java 文件
