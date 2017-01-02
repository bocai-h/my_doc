# rails进阶

要理解rails的设计思想和实现架构,首先要对Rack有一个清晰的认识,因为rails是一个就是一个Rack应用.它离不开Rack的设计模式.所以要搞清Rails还是先搞懂Rack.


- Rack的设计意图与实现模式
> Rack本身作为web应用与web服务器的中间层,核心目的是隔离不同的webserver的实现差异以及为web应用提供一个屏蔽webSever的抽象环境.

- Rack实现方法
> [ruby rack inside](http://pothibo.com/2013/11/ruby-on-rails-inside-actiondispatch-and-rack/)
  [ruby rack middleware](https://www.amberbit.com/blog/2011/07/13/introduction-to-rack-middleware/)

- Rack的实现模式
> 1. web server的抽象
     Rack对于webserver的抽象层面很高,它并不队webapp提供webserver的抽象,而是把webserver的一些重要信息和HTTP协议封装在一个env对象中进行抽象.应用只需要访问env对象就能得到几乎所有的环境信息
 > 2. 中间件模式 
   在web应用中有一些功能是很常用的,比如静态文件处理,压缩功能,url路由等等.由于这些功能如此常用和独立,显而易见我们每个人不可能为这些功能重复造轮子.类似的,其实我的app和前面的常用功能在处理层面上是平行的.所以Rack在设计上,不仅为我们提供了webserver的抽象海童工一种能打包独立功能和重用这些功能的机制.Rack用装饰器模式来实现这种功能,每个独立的功能叫做中间件(middleware).试着对你的rails项目执行**rake middleware**你会看到当前Rails项目所使用的所有中间件,从这点我们可以看成,**Rails app不过是一系列的Rack中间件的组合**.

- Rack封装web功能
> Rack把很多常用的web功能都做成中间件,包含在Rack项目中了,比如Etag,SendFile,Directory

-. 中间件
> 由于所有web app的功能都是由不同中间件组成,那么这些中间件之间必须遵循同意的接口规范
> Rack的所有中间件包括app(最里面的中间件都是一个ruby对象),接口规范为: 这个对象必须能够响应.call(env)方法
  env就是当前的环境,.call方法返回一个三元数组,只接手一个env参数,返回一个三元数据.1.HTTP响应码,2.响应头->Hash,3.响应body对象,需要能够有.each方法
 总结: Rack本质 1.为app的托管环境,屏蔽webServer 2.提供了一个给予装饰者模式的中间件机制,为应用的实现提供了一种灵活的可复用的架构,这种方式本身也是对HTTP处理流程的抽象.


- ActiveSupport Gem
> 提供了一些工具类和对内置类型的monkeypatch
  autoload重写了autoload Rails中大量使用,不需要第二个文件参数,根据默认规则自动加载文件

- ActionPack Gem
>Action Pack is a framework for handling and respond to web requests.
>主要包含三部分
>1. 提供路由机制ActionDispatch
>2. 提供controller基类ActionController
>3. 文件渲染Render
> ###ActionDispatch::Joureny
分析参考 [https://ruby-china.org/topics/30929](https://ruby-china.org/topics/30929)
