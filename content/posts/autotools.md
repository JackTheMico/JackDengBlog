+++
title = "记录下我曾经用过或接触过的自动化工具"
author = ["Jack Deng"]
date = 2020-05-26T00:00:00+08:00
tags = ["python", "auto"]
categories = ["tools"]
draft = false
+++

## RobotFramework {#robotframework}

[Github 地址](https://github.com/robotframework/robotframework)
Python 语言实现，常用来做App 自动化测试、接口自动化测试、浏览器相关的自动化操作。使用专门的 .robot 脚本来编写自动化的操作，操作浏览器需要安装 Selenium 插件包并设置相应浏览器的 WebDriver 。感觉使用起来比较麻烦。有个专门的IDE：[RIDE](https://github.com/robotframework/RIDE)


## AutoMagica {#automagica}

[Github Page](https://github.com/automagica/automagica)
也是Python 的一个项目，可以完成操作浏览器、excel 、自动发送微信等工作，可以使用其 Recorder 根据截图来生成移动、点击鼠标等等代码，使用比较方便，但是操作间有延迟，感觉性能不太好。另外 Recorder 会将截图上传至公网，故涉密的界面操作不能使用 Recorder 截图来定位。


## AirTest {#airtest}

[官网](http://airtest.netease.com/)
网易爸爸推出的跨平台UI 自动化编辑器，几乎带UI 的任何东西都能操作，暂时没用过，看上去比 robotframework 好用，待定。
