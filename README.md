# 项目背景
Emuelec是基于amlogic晶晨芯片制作的游戏系统。

主要用于双系统装在电视盒子上。由于游戏内容较大需要外接存储设备。

但是外接存储设备在异常拔出情况下会无法自动进入外接系统设备。

因此需要在电视盒子主系统安装tf卡引导程序，来进入外接存储设备。

但是tf卡引导程序由于安卓权限问题，需要root才能使用。

# 项目逻辑
因此通过该项目以实现非root进行tf卡引导程序功能。

思路很简单：电视盒子的开发者模式无需验证码，只要开一次每次开机都会进入adb调试模式

那么就可以通过调用安卓frp将本地的adb端口映射到windows的服务器上

再通过windows调用adb指令来完成tf卡引导功能。

本项目为了快速实现功能，通过拉取frp-Android项目，在项目上二开完成功能

本项目为个人自用，因此是二开的frp-Android。

如果该项目能够帮到你，我将根据逻辑进行重构，以提高项目性能以及使用体验

# frp-Android
A frp client for Android  
一个Android的frpc客户端

## 编译方法

如果您想自定义frp内核，可以通过Github Actions或通过Android Studio编译

### 通过Android Studio编译

1. 在项目根目录创建apk签名密钥设置文件```keystore.properties```，内容参考同级的```keystore.example.properties```
2. 使用Android Studio进行编译打包

## 常见问题
### 项目的frp内核(libfrpc.so)是怎么来的？
直接从[frp的release](https://github.com/fatedier/frp/releases)里把对应ABI的Linux版本压缩包解压之后重命名frpc为libfrpc.so  
项目不是在代码里调用so中的方法，而是把so作为一个可执行文件，然后通过shell去执行对应的命令  
因为Golang的零依赖特性，所以可以直接在Android里通过shell运行可执行文件

### 开机自启与后台保活
按照原生Android规范设计，如有问题请在系统设置内允许开机自启/后台运行相关选项
