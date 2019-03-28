---
title: 日常-论如何防止同学玩电脑
date: 2019-03-27 21:07:07
tags: 日常
---
我们大六班的同学们浪的可是名不虚传
每天，教室里都会传来响亮的[《Hop》](https://music.163.com/#/song?id=561493928) 
作为~~不称职的~~电脑管理员，当然要好好管制。当然，不能硬来，要想点"软"的方法。 
于是，就有了这个神奇的企划,它分为三个部分：
  1. DNS纂改（防止外网）
  2. 禁止修改壁纸
  3. 防止进入隐私浏览

Part.1 DNS纂改 
  毕竟我不可能直接改动学校网，所以只能在本机上懂手脚，直接修改Hosts文件。
  但一次次的手动改，实在麻烦（~~懒癌晚期~~）。于是乎就写了个这样的脚本。
  ```
  @echo off
  del hosts
  curl https://raw.githubusercontent.com/hanbing1122/soup-blocklist/master/hosts >> hosts
  copy hosts C:\Windows\system32\drivers\etc\
  ipconfig /flushdns
  ```
然后拖到"启动"文件夹里，就能实现开机启动了。

Part.2 禁止修改壁纸
  虽然这个在组策略里可以改，但我希望能一条命令解决，于是就写了条注册表:
  ```
  Windows Registry Editor Version 5.00
  
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\ActiveDesktop] "NoChangingWallPaper"=dword:00000001
  ```
Part.3 防止进入隐私浏览
  这个在Chrome的设置里还真找不到，但是还是Google到了一个[solution](https://www.technipages.com/chrome-disable-incognito-mode)
  同样是写一条注册表
  ```
  Windows Registry Editor Version 5.00

  [HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome] "IncognitoModeAvailability"=dword:00000001
  ```
这样的办法只 work 了几天。
某滑稽陈同学就找到了 solution （用U盘把 Hop 的 MV 拷进来）。
最后只能释出 final 方案————设密码(所以之前的方法都没什么鬼用了…………)

Finally，希望这件事情能圆满完结。

附近期命令执行history排行
![history](https://pic.superbed.cn/item/5c9b837b3a213b04173873ee)
