# Rails::Engine

Rails::Engine允许你包裹一个特定的Rails应用或者功能性子集与别的应用一起共享或者打包在一个更大的应用里.每个Rails::Application仅仅只是一个允许一些简单特性和应用共享的engine.

任何Rails::Engine也是一个Rails::Railtie,所以在railties里面相同的方法(像 rake_tasks和generators)和配置选项在engines中也是可用的

. 创建一个Engine

如果你想一个gem的行为像一个engine,你可以指定一个Engine给它并把这些放在你的plugin的lib文件夹中(和我们指定一个Railtie一样)

~~~~
# lib/my_engine.rb
module MyEngine
 class Engine < Rails::Engine
 end
end
~~~~

然后保证这个文件在你的config/application.rb之前被载入(或者在Gemfile之前),models,controllers和helpers会自动载入app内,载入路由是在config/routes.rb,
载入locales在config/locales/*,载入tasks在lib/tasks/*

- 配置
此外Railtie的配置是通过application共享的,在一个Rails::Engine,你可以访问autoload_paths,eager_load_paths和autoload_once_paths.这点和Railtie不同,在当前engine的范围内

~~~~
class MyEngine < Rails::Engine
  #Add a load path for this specific Engine
  config.autoload_paths << File.expand_path("../lib/some/path",__FILE__)
 initializer "my_engine.add_middleware" do |app|
   app.middleware.use MyEngine::Middleware
 end
end
~~~~

- Generators
你可以通过config.generators方法给engines设置一个generators

~~~~
 class MyEngine < Rails::Engine
   config.generators do |g|
     g.orm      :active_record
     g.template  :erb
     g.test_framework :test_unit
   end
 end
~~~~

你也可以给一个应用生成一个generators

~~~~
 class MyEngine < Rails::Engine
   config.app_generators.orm :datamapper
 end
~~~~

更过内容  [rails官方文档](http://api.rubyonrails.org/)
.......

