---
layout:       post
title:        "git.io 搭建"
author:       "cyalcher"
header-style: text
catalog:      true
tags:
    - git blog
    - git pages
---
# 结论
建repo，加样式，本地测试，写文档。
# 一、背景
一直想记录下自己的学习记录，2024.04开始了。<br>
开发本：macos 13.5.1。<br>

# 二、目标
完成个人的blog可访问；
# 三、实施过程
## 3.1 创建repo
建repo，建html，测试可访问 ，done;以下3步：<br>
① 建repo：创建1个和自己github 的user_name一致的repo。 <br>
![create repo](./img/in-post/0413_blog_start.png) <br>
② 建html：创建index.html; <br> 
**注意看下自己repo默认的repo**
```
$ cd {Owner}.github.io
$ echo "Hello World!" > index.html
$ git add index.html
$ git commit -m "Init commit"
$ git push origin main
```
③ 访问test：访问域名；<br>
https://{Ower}.github.io/
## 3.2 加主题
fork 主题repo(Huxpro)；改配置；加个人repo；<br>
① 在github直接fork Huxpro <br>
② 在Huxpro的repo中修改_config.yml文件；还要修改index.html; <br>
③ 在Huxpro中加自己的repo <br>
```
$ git remote add mine https://github.com/{owner}/{owner}.github.io
```
## 3.3 写markdown文档
写文档可以用开发的ide就可以；我用的vscode，还是挺好用的，提交测试； <br>
## 3.4 本地查看
本地查看这个是快速验证，预览的； <br>
## 3.5 坑简记
1. 注意添加repo 是在 主题repo中添加自己得repo; <br>
2. 本地快速预览验证使用 Ruby，install的时候坑比较多，根据报错不断修改版本；<br>



# 参考
[如何快速搭建自己的github.io博客](https://keysaim.github.io/post/blog/2017-08-15-how-to-setup-your-github-io-blog/)
