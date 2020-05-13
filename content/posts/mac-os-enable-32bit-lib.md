---
title: "Mac OS 开启32位编译支持"
date: 2020-05-13T10:10:12+08:00
draft: true
---

做CMU-15-213的Lab的过程中发现，我在Mac OS下用make命令编译源代码会出错，错误如下：

```
ld: symbol(s) not found for architecture i386
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

错误说的是没有i386架构的支持，查看源代码的Makefile，确实有-m32的flag，也就是以32位架构进行编译
网上查询一番发现，Mac OS从10.14，即Mojave开始放弃了对32位架构的编译支持，也就是说虽然可以运行32位程序，但是不能编译

解决方法如下：
在终端运行命令
```
open /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg
```
安装后就可以开启对32位的编译支持了，之后便可以正常编译32位程序，不过会抛出一条警告
```
ld: warning: The i386 architecture is deprecated for macOS (remove from the Xcode build setting: ARCHS)
```
编译器抱怨说i386架构已经被废弃啦

参考：
> [Can't compile C program on a Mac after upgrade to Mojave](https://stackoverflow.com/questions/52509602/cant-compile-c-program-on-a-mac-after-upgrade-to-mojave/52530212#comment91963866_52509602)
