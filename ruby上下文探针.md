# instance_eval VS class_eval

instance_eval和class_eval都是作为上下文探针的作用,但是它们之间有细微的区别.这也是作为面试常问的一个问题.

## instance_eval
*使用instance_eval为对象定义单例方法*

~~~~
class A
end

a = A.new
a.instance_eval do
  self  # => a
  # current class => a's singleton class
  def method1
    puts 'this is a singleton method of instance a'
  end
end

a.method1
#=> this is a singleton method of instance a

b = A.new
b.method1
#=>NoMethodError: undefined method `method1' for #<A:0x10043ff70>

~~~~
*使用instance_eval为类定义单例方法(原理:类也是Class类的实例)*

~~~~
  class A
end

A.instance_eval do
  self  # => A
  # current class => A's singleton class
  def method1
    puts 'this is a singleton method of class A'
  end
end

A.method1
~~~~

## class_eval

*使用class_eval为类定义实例方法*

~~~~
class A
end

a = A.new
a.method1
#=> NoMethodError: undefined method `method1' for #<A:0x10043ff70>

A.class_eval do
  self  # => A
  # current class => A
  def method1
    puts 'this is a instance method of class A'
  end
end

a.method1
#=> this is a instance method of class A
~~~~

## 总结
instance_eval必须由instance来调用,可以用来定义单态函数singleton_methods
class_eval必须是由class来调用,可以用来定义实例函数instance_methods

## 区别
- intance_eval由实例调用,class_eval必须由类来调用
- instance_eval的block内直接定义方法为方法接收者单例方法(根据对象不同可能是实例方法或者类方法),class_eval的block里面直接定义方法由于其调用者只能是类,所以均为实例方法.当然定义方法前方法名前家self.则定义的是类方法