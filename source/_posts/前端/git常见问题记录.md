---
title: Git常见问题记录
date: 2025-01-24 11:03:51
tags:
	- git
categories:
	- 前端
---

### 一、Failed to connect to github.com port 443 after 21084 ms: Couldn‘t connect to serve

Git报错：`Failed to connect to github.com port 443 after 21084 ms: Couldn't connect to serve`
当使用clone、pull、push等git命令的时候出现上述报错信息，大概率是由于开了代理的问题。解决方式如下：

1. 解决方式一：关闭代理
首先，关闭本地的代理，可以通过计算机系统自带的代理设置查看当前代理是否开启。

如果本地的代理都已经关闭，则尝试把 git 配置的代理进行关闭（如果只是修改当前的项目，那么可以不用–global修改全局）。

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

注意把自己的代理软件也都关闭，然后重新打开下项目（不重新打开项目有时候会出现编辑器配置修改了没有生效的问题）。
如果不行的话尝试下刷新DNS缓存，用cmd打开windows命令窗口，输入：

`ipconfig/flushdns`

如果还是不行就使用第二种方式（本人用第二种方式解决的）

2. 解决方式二：开启代理

第一种方式是关闭git的配置代理，第二种方式是开启代理。代理加速器继续开着，然后查看当前本地的代理IP+端口是多少。查看方式如下：

2.1 搜索代理服务器设置


2.2 查看IP 和端口


2.3 给git配置设置代理


2.4 给git配置设置代理
（注意：记得端口用自己实际的端口，然后不需要修改全局的git的话就把–global不写，这样只修改当前项目的git配置项，取消代理那个不要加哈，我这写上去是为了让大家知道加了代理后怎么取消）

```
# 设置代理
git config --global http.proxy http://127.0.0.1:33210
git config --global https.proxy http://127.0.0.1:33210

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```



这样就完成了，一般来说这样就可以了。（自己本人第一种方式没成功，用了第二种方式成功了）
                        
原文链接：https://blog.csdn.net/qq_43651168/article/details/131074308
