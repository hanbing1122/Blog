---
title: 博客数据迁移记录
date: 2019-03-30 09:15:57
tags:
---

这个博客一开始是搭建在 Coding 的 Cloud Studio上。
前几天突然脑子一热把博客源文件备份到了 Github 上。

然后……第二天 Cloud Studio 就崩溃了。
![驾崩](https://dn-coding-net-tweet.codehub.cn/photo/2019/dc08cc20-8277-4fd3-bf34-aa14a629ada3.png)
加上前几天一键部署功能突然失效……看来不只是我的问题……
![问题](https://ww1.sinaimg.cn/large/007i4MEmly1g1kk6k7o3kj31070jx40r.jpg)
最后想想……还是把数据存本地更好一些.

毕竟我已经把数据放到 Github 上了，所以直接 Clone 下来就完事.
```
git clone https://github.com/hanbing1122/Blog.git
```
然后安装[NodeJS](https://nodejs.org/zh-cn/download/)，一直下一步即可。
其他步骤照旧，只是先要设置 npm 的镜像（天朝的网实在太慢……）
```
npm config set registry https://registry.npm.taobao.org
npm install hexo
npm install
npm install hexo-deployer-git
```
然后就可以 hexo server 试试
但是（对于我）会出现一个问题：打开一片空白
这是因为 Github 同步的时候并没有把主题同步上去
所以需要重新下载主题并拷贝到 themes 文件夹中。

在编辑完成后，直接执行 hexo deploy 就可以。
在 deploy 的时候，还会遇到一个问题
![问题2](https://ww1.sinaimg.cn/large/007i4MEmly1g1kkmc2liuj30kn0chq3j.jpg)
直接按照提示照做：
```
git config --global user.email "xxx@example.com"
git config --global user.name "xxx"
```

在 hexo deploy 完成后
```
git add .
git commit -m "更新Hexo源文件"
git push origin master
```