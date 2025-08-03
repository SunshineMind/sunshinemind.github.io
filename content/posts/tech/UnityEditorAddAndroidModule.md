---
date: '2025-08-03T16:36:18+08:00'
draft: false
title: 'Unity 编辑器添加安卓模块无法找到 JDK SDK NDK 问题'
lastmod: 2025-08-03T16:36:18+08:00

categories:
- Unity

tags:
- Unity Hub
- Unity Editor
- Android
---

### 背景

在 Windows 平台，使用 Unity Hub 3.5.0 给已经安装的 Unity Editor 2022.3.63f1 添加 Android 模块后，此版本编辑器不存在 JDK SDK 与 NDK。

在资源管理器中验证，确实此版本路径下的```Data/PlaybackEngines/AndroidPlayer/```下不存在SDK、NDK、OpenJDK这个几个目录。

### 原因猜测

安装时，网络质量不好，多次出现下载失败，也点击了多次重试。
Android Build Support被安装时，可能有路径下覆盖的行为，导致更显解压出的OpenJDK、SDK、NDK文件被覆盖。

出现这个情况后，尝试在Unity官网下载对应编辑器版本的Android Build Support离线安装exe包进行安装，也没有解决（这个包可能根本就不包含OpenJDK、SDK和NDK）。

### 解决方案

使用 Unity Hub 给某一个版本的 Unity Editor 添加安卓模块/负载时，建议只勾选 Android Build Support 选项并安装，等待安装结束后，再勾选添加 OpenJDK 与 Android SDK & NDK Tools 选项安装。

### 后续

~~翻阅 Unitt Hub 发布说明，这个问题应该在下一个版本 3.5.1 就被修复，未验证，但我的其他设备一直在用最新版的 Unity Hub 没出现过这个问题。~~ 看错了。