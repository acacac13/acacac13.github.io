---
title: 解决hexo d 报超时的问题
date: 2021-04-25 19:48:40
tags: hexo
categories: problem
---

# 1、问题

> 运行hexo d时报错

![image-20210425194953535](https://gitee.com/acacac13/images/raw/master/20210425194953.png)

> 报错可以看出是连接超时的问题

# 2、解决

> 找到git的安装目录，找到ssh_config文件，使用记事本打开

![image-20210425195146015](https://gitee.com/acacac13/images/raw/master/20210425195146.png)

> 把如下内容复制到ssh_config文件中

```
Host github.com
User git
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443
```

> 添加完成后如下图

![image-20210425195319230](https://gitee.com/acacac13/images/raw/master/20210425195319.png)

> 再次输入 hexo d 即可顺利运行

![image-20210425195421262](https://gitee.com/acacac13/images/raw/master/20210425195421.png)