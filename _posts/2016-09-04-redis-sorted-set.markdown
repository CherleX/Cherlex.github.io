---
layout: post
title:  "使用Redis Sorted Set 实现优先队列"
date:   2016-09-04 14:12:26
categories: Redis
tags: Redis Sorted-Set
---

* content
{:toc}
判断二叉树是否对称。


# 优先级队列需求 #
- 用户发起任务会指定一个权重，权重越大优先级越高
- 权重相等的任务，时间越早优先级越高


## 权重计算规则 ##
- 用户指定的权重为基础权重，使用base_score表示，时间转换后的权重使用time_score表示
- 那么任务的权重可以表示为score = base_score + time_score
- score的数值越大优先级越高（要求时间和time_score成反比）


## time_score 计算方法 ##
```Ruby
time_base_line = 10 **（Time.now.to_i.to_s.size - 1） #和Time.now是同一个数量级
time_score = time_base_line / Time.now.to_f
```
比如：
```Ruby
puts(Time.now.to_f)
puts(time_base_line / Time.now.to_f + base_score)
sleep(0.001)
puts(time_base_line / (Time.now.to_f) + base_score)
```
输出：
```Ruby
1473046085.6919649
50.678865386298874 #时间早，权重大
50.67886538629841  #时间晚，权重小
```


## 数据结构设计 ##

- 原有的数据结构不动
- 新增一个Sorted Set用于存储优先级
 > value:存储task_id  
 > score:存储task的权重


## Redis Sorted Set 读取权重最大的value ##
> Sorted Set 是递增排序的，所以权重最大的value在最后


```
ZRANGE hlt_task -1 -1
```

数据库的数据：

|row|value|score|
|:--|:--|:--|
|1|late|50.678866248082244|
|2|early|50.67886624808317|

命令输出：

```
127.0.0.1:6379> ZRANGE hlt_task -1 -1
1) "early"
```



