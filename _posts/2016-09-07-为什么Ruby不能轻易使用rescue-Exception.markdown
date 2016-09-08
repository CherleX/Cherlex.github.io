---
layout: post
title:  "为什么Ruby不能轻易使用rescue Exception？"
date:   2016-09-08 14:12:26
categories: Ruby
tags: Ruby 多线程
---

* content
{:toc}
关于Ruby Exception要知道的细节





# 关于Exception

在Ruby中，Exception是所有异常的基类，也就意味着rescue Exception包括了所有可能的异常，甚至包括了：

`SyntaxError`, `LoadError`,  `Interrupt` 。

 rescue `Interrupt` 会阻止用户使用 `CTRL C` 来退出程序。

rescue `SignalException`  会阻止程序正确地响应信号，比如：除非使用`kill -9`，否则无法终止。

rescue `SyntaxError` 意味着使用`evel ` 发生了错误也不会发出告警。

下面这个例子，诠释了上述三种情况：

```ruby
loop do
  begin
    sleep 1
    eval "djsakru3924r9eiuorwju3498 += 5u84fior8u8t4ruyf8ihiure"
  rescue Exception
    puts "I refuse to fail or be stopped!"
  end
end
```

这个程序在运行的时候，我们无法使用 `CTRL C` 来中断执行。

rescue 默认并不是捕获Exception，比如

```ruby
begin
  # iceberg!
rescue
  # lifeboats
end
```

默认的写法会捕获 `StandardError` ，而不是`Exception`。通常来说，我们应该捕获比 `StandardError` 更具体的异常，如果捕获Exception是扩大了错误范围而不是缩小，这会导致我们更难准确定位bug。

# 正确用法

捕获 `StandardError` 的通常做法是：

```ruby
begin
  # iceberg!
rescue => e
  # lifeboats
end
```

它和下面的用法是等价的：

```ruby
begin
  # iceberg!
rescue StandardError => e
  # lifeboats
end
```

但是，在个别情况，处于记录日志的目的，也会捕获Exception，同时重新抛出异常。

```ruby
begin
  # iceberg?
rescue Exception => e
  # do some logging
  raise e  # not enough lifeboats ;)
end
```



> 参考：[Why is it bad style to `rescue Exception => e` in Ruby?]( http://stackoverflow.com/questions/10048173/why-is-it-bad-style-to-rescue-exception-e-in-ruby)









