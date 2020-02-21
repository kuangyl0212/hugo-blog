---
layout: post
title: "Mac OS开启NTFS分区的索引"
date: 2020-02-21T13:15:38+08:00
---

安装Alfred之后发现搜索不到ntfs分区上的文件，后来发现Alfred文件搜索实际上是调用Spotlight，因此只要spotlight可以搜索ntfs分区就可以了

默认情况下，spotlight不会对ntfs分区建立索引，因此需要手动开启。

Mac OS自动一个工具mdutil可以完成这个操作。

使用-s参数可以查看一个分区的索引情况，如果这个分区没有索引会返回“Indexing disabled”：

'''
mdutil -s /Volumes/DRIVE_NAME
'''

可以用下面的命令开启一个分区的索引：

'''
sudo mdutil -i on /Volumes/DRIVE_NAME
'''
这个时候你再用上面的-s命令就可以看到“Indexing enabled”了。如图：

![indexing enabled](https://tva1.sinaimg.cn/large/0082zybply1gc3yqasxopj30pk064wf9.jpg)

然后需要重建索引：
'''
mdutil -E /Volumes/DRIVE_NAME
'''

但是重建索引不会马上生效，需要重启一下，或者等操作系统的计划任务，总之过一段时间就可以了

索引生效以后，spotlight就可以搜到ntfs分区上的文件了，Alfred也一样。

> 本文参考：[How to index a NTFS partition on Mac](https://christianfei.com/posts/enable-indexing-of-ntfs-partition-on-mac/)
