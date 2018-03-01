---
layout:     post
title:      mongodb安装笔记
subtitle:   微生物学习笔记
date:       2018-02-09
author:     zd200572
header-img: img/post-bg-alitrip.jpg
catalog: true
tags:
    - mongodb

---

参考自：https://www.cnblogs.com/weixuqin/p/7258000.html

`brew install mongodb`

如果报错：

```
mongodb: A full installation of Xcode.app 8.3.2 is required to compile this software.
Installing just the Command Line Tools is not sufficient.
Xcode can be installed from the App Store.
Error: An unsatisfied requirement failed this build.
```

 

说明Xcode版本过低，需要更新，如果你不想更新，可以通过使用命令：

```
homebrew search mongodb
```

查看更低版本的MongoDB，然后安装更低版本的MongoDB。

```
brew install mongodb@3.4
```

启动MongoDB服务：

```
brew services start mongodb@3.4
```

关闭MongoDB服务：

```
brew services stop mongodb@3.4
```

进入MongoDB图形化界面：

```
mongo
```

查看homebrew安装的服务情况：

```
brew services list
```

```sh

If you need to have this software first in your PATH run:

  echo 'export PATH="/usr/local/opt/mongodb@3.4/bin:$PATH"' >> ~/.zshrc

To have launchd start mongodb@3.4 now and restart at login:

  brew services start mongodb@3.4

Or, if you don't want/need a background service you can just run:

  mongod --config /usr/local/etc/mongod.conf

```




**我的个人博客 **：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)



