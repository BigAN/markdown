---
title: "kafka"
date: 2015-05-27 12:10
---

关系 
    
    sset_topic_partitions 指定fetch 然后调用task_done 来指定 task_done 最后 commit 才更新 commit 值。这时才能从头开始读取。

问题

其他机器访问不了。看下是不是 域名没有解析，在该机器上。
