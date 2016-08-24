# ruby调试工具

- pry

- pry-byebug([github地址](https://github.com/deivid-rodriguez/pry-byebug))
> 正常使用binding.pry,代码执行会停在binding.pry的后一句.执行step,如果是function就会进入function

~~~~
def some_method
  puts 'Hello World' # Run 'step' in the console to move here
end

binding.pry
some_method          # Execution will stop here.
puts 'Goodbye World' # Run 'next' in the console to move here.

~~~~

- pry
> 在pry的断点中运行命令disable-pry会直接退出断点,对于多次循环的断点有奇效

- pry-doc
> 配合pry可以查看方法的注释和源代码,大部分情况下都比较准确

~~~~
 #提供show-doc(?)和show-source($)两个方法
 a = [1,2,3]
? a.size    #返回对size方法的解释和举例
$ a.size    #返回size方法的c源码
~~~~