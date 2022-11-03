---
title: Mac使用问题
date: 2018/12/23 20:13:56
tags: Config
categories: Config
---

1.  `sudo spctl --master-disable`
2. “系统偏好设置”--“安全与隐私”。在“通用”一览中，会看到“允许从以下位置下载的应用：”设置。这个时候应该已经有了三个可选项：“App Store、App和被认可的开发者、任何来源”。
3. 解锁后选择 “任何来源”
4. 休眠后没有声音 sudo killall coreaudiod
5. 修改环境变量 export PATH=/Users/wangyulong/Downloads:$PATH
