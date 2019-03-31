---
title: 博客数据迁移记录
date: 2019-03-30 09:15:57
tags:
---

这个博客一开始是搭建在 Coding 的 Cloud Studio上。
然后某一天 Cloud Studio 自己崩溃了。
![驾崩](https://dn-coding-net-tweet.codehub.cn/photo/2019/dc08cc20-8277-4fd3-bf34-aa14a629ada3.png)
不过好在之前已经把博客的源文件备份到了 GitHub 上，并没有造成什么损失。
为了防止类似事件发生，我决定把 hexo 部署到本地.
毕竟在前面已经备份到了 GitHub 上，so：
```
git clone https://github.com/hanbing1122/Blog.git
```
然后安装[NodeJS](https://nodejs.org/zh-cn/download/)，一直下一步即可。
其他步骤照旧，只是先要设置 npm 的镜像（天朝的网实在太慢……）
```
npm config set registry https://registry.npm.taobao.org
npm install hexo（可能需要加 --save，不确定）
npm install
npm install hexo-deployer-git
npm install hexo-server（P.S. 我在自己的服务器上(Debian 9)上安装时不能执行 hexo server，执行此命令后正常）
```
随后可以尝试 hexo server，不出所料打开会一片空白
这是因为 Github 同步的时候并没有把主题同步上去
~~所以需要重新下载主题并拷贝到 themes 文件夹中。~~
[解决 themes 丢失问题](http://w4lle.com/2016/06/06/Hexo-themes/index.html)

在同步到 Github 前有一个坑：没有CNAME文件。
Github 会在绑定域名时自动创建这个文件。
但是我本地服务器上没有这个文件。在同步后网站会 404
直接在 source 文件夹中创建一个：
```
soup.cf
```

随后 hexo deploy。在 deploy 的时候，可能还会遇到一个问题
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
就可以完成备份.
