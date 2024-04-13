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



# 参考
[如何快速搭建自己的github.io博客](https://keysaim.github.io/post/blog/2017-08-15-how-to-setup-your-github-io-blog/)
