# Rails view路径扩展

Rails项目中有些视图并不在app下的view下的时候,比如插件中的views会在lib目录下,这时候我们render的时候就找不到了.

我们可以通过扩展视图的寻找路径去解决这个问题,具体配置如下:

~~~~
 #application.rb
 
  config.paths["app/views"] << "#{Rails.root}/lib/my_plugin/ acts_as_multilingual/app/views"
  
~~~~

[rails渲染模板的过程](http://climber2002.github.io/blog/2015/04/06/digging-rails-how-rails-finds-your-templates-part-4/)