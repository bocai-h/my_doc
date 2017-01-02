# rails技巧之tap

tap是rails开发过程很常用的方法,在调试和写出简洁代码上有着不错的发挥

从tap的Api可以看出,tap是Object的instance_method,传递self给一个block,最后返回self

~~~~
  Object.instance_methods.grep(/^tap/)  #[:tap]

~~~~

tap源码

~~~~
 def tap
  yield self
  self
 end
~~~~

用法一: 调试.当你使用链式方法发生错误时,如果需要测试这个过程中哪个出了问题,一般的做法是拆断这个方法,设置中间变量,接着测试中间变量是否正确,如果正确,则把变量换个地方继续测试,方法很长时就没法测了,当然ruby为你想好了,有着优雅又简便的实现

~~~~
 %w(x y z).push('a').shift.upcase.next  #=> "Y"

# 里面的x就代表此时的self
 %w(x y z).push('a').shift.tap{|x| p x}.upcase.next #=> "Y" 

~~~~
用法二:简化代码.我们构建一个方法想返回一个String/Array/Hash之类结果,一般做法是先定义一个变量,结果把运算结果赋值给这个变量,接着返回变量,用tap一部搞定,其实就是源码意思的实现

~~~~
 [].tap {|i| i << "abc"}
''.tap{|i| i << do_some_thing }
~~~~