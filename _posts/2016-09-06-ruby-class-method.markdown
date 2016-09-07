---
layout: post
title:  "Ruby 定义类方法的 n 种姿势"
date:   2016-09-06 14:12:26
categories: Ruby
tags: Ruby 
---

* content
{:toc}
关于 Ruby 类方法的定义和使用



# 什么是类方法

在大多数情况下，我们调用一个类的方法，是依附于类的某个实例的，比如：

```ruby
Person.new().to_s
```

但是，有些时候我们调用一个类并不意味着一定要实例化这个类。例如，在使用Ruby自带的File类打开一个文件，我们是需要实例化File的对象的。但是在删除某个文件的时候，其实并没有打开这个文件，自然也就不存在这个类的对象了。这时候，我们使用类方法是更合适的。删除一个文件，直接传入文件名：

```ruby
File.delete('test.rb')
```



# 类方法和实例方法的区别

最大的区别当然就是使用的区别。类方法可以直接使用，而实例方法必须通过类的对象来调用。同时，类方法和实例方法的定义也是有区别的。下面是个简单例子：

```ruby
class Example
  def instance_method		#instance method
  end
  
  def Example.class_method	#class method
  end
  
end
```



# 类方法怎么定义

- 最基本的2中定义方式

  ```ruby
  #1
  class Person
    def self.species
      "Homo Sapien"
    end
  end
  #2
  class Person
    def Person.species
      "Homo Sapien"
    end
  end
  ```

- 类似于继承的2种定义方式

  ```ruby
  #3
  class Person
    class << self
      def species
        "Homo Sapien"
      end
    end
  end
  #4 
  class << Person
    def species
      "Homo Sapien"
    end
  end
  ```

- 元编程的2种定义方式

  ```ruby
  #5
  Person.instance_eval do
    def species
      "Homo Sapien"
    end
  end
  #6
  class Foo
  end
  metaclass = (
  class << Foo;
    self;
  end)
  metaclass.class_eval do
    def species
      "Homo Sapien"
    end
  end
  ```


# 类方法怎么使用

类方法的使用非常简单，直接通过类进行调用即可。比如：

```ruby
File.delete('test.rb')
Time.now
String.try_convert("str")
```

