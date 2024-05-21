---
title: MacBook Pro降级到Catalina版本
date: 2024-02-02 16:19:34
description: MacBook Pro降级到Catalina版本
keywords: MacBook Pro降级到Catalina版本
tags:
categories:
top_img: false
cover: false
---

MacBook Pro (15 英寸，2017) 降级到Catalina版本



#### MacBook Pro版本

**13-inch, 2017, Four Thunderbolt 3 Ports**

#### 降级系统

**macOS Catalina 10.15.7**  [Catalina 10.15](macappstores://apps.apple.com/cn/app/macos-catalina/id1466841314?mt=12)





使用“终端”创建可引导安装器

```sh
sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```



1. 将 USB 闪存驱动器接入 Mac。
2. 打开“应用程序”文件夹内“实用工具”文件夹中的“终端”。
3. 在“终端”中键入或粘贴[以下命令](https://support.apple.com/zh-cn/101578#commands)下述每个命令都假设安装器位于你的“应用程序”文件夹中，并且“MyVolume”是你所使用的 USB 闪存驱动器或其他宗卷的名称。如果宗卷不是这个名称，请将命令中的 `MyVolume` 替换为相应名称。
4. 当系统提示你键入管理员密码时，请照做。在你键入密码时，“终端”不会显示任何字符。然后按下 Return 键。
5. 当系统提示键入 Y 来确认你要抹掉宗卷时，请照做，然后按下 Return 键。在抹掉宗卷的过程中，“终端”会显示进度。
6. 宗卷被抹掉后，你可能会看到一条提醒，提示“终端”要访问可移除宗卷上的文件。点按“好”以允许继续拷贝。
7. 当“终端”显示操作已完成时，相应宗卷将拥有与你下载的安装器相同的名称，例如“安装 macOS Sonoma”。你现在可以退出“终端”并弹出宗卷。



重启电脑

{% label ⌘ blue %} {% label R blue %}



选项按钮

 

磁盘工具



Macintosh HD



抹掉



[创建可引导的 macOS 安装器](https://support.apple.com/zh-cn/101578)



时间机器备份



