# BDD(Behavior-driven Develop:行为驱动开发)

+ TDD(Test-driven Develop:测试驱动开发)
  > 是敏捷开发中的一项核心实践和技术,也是一种设计方法论。TDD的原理是在开发功能代码之前，先编写单元测试用例代码，测试代码确定需要编写什么产品代码。TDD虽是敏捷方法的核心实践，但不只适用于XP（Extreme Programming），同样可以适用于其他开发方法和过程。

+ BDD 是TDD的一个变种.
 > 行为驱动开发是一种敏捷软件开发的技术，它鼓励软件项目中的开发者、QA和非技术人员或商业参与者之间的协作。BDD最初是由Dan North在2003年命名，它包括验收测试和客户测试驱动等的极限编程的实践，作为对行为驱动开发的回应。在过去数年里，它得到了很大的发展。

+ BDD过程
 > 遇红(失败的测试)  --  变绿(写实现让测试通过)  -- 重构(改变实现方式,如消除代码重复)
+ Rspec(Request Spec)
> 模拟用户在浏览器上的操作与应用程序进行交互

+ Rspec
>    
       group :development,:test do
         gem 'rspec-rails', '~> 3.5'
       end
	   bundle install  #Initialize the spec/ directory (where specs will reside) 
       rails generate rspec:install
       bundle exec rspec  #se the rspec command to run your specs
       #By default the above will run all _spec.rb files in the spec directory
       # Run only model specs
       bundle exec rspec spec/models
       # Run only specs for AccountsController
       bundle exec rspec spec/controllers/accounts_controller_spec.rb


+ capybara
> Capybara helps you test web applications by simulating how a real user would interact with your app.
 通过模拟真实用户交互的方式来测试你的 web 应用。它内置 Rack::Test 和 Selenium 支持，也支持其他驱动。WebKit 通过外部 gem 的形式支持。
   

+ capybara用法
>
	 group :develop,:test do
	  gem 'capybara', '~> 2.7', '>= 2.7.1'
	end    
    #If the application that you are testing is a Rails app, add this line to your test helper file:
    require 'capybara/rails' 

+ guard
  > guard是一个自动测试的工具,其内包含了强大的一个gem包(listen),可以监听文件的变动,然后自动运行测试.

+ guard用法
> 
	 group :develop,:test do
	   gem 'guard', '~> 2.14'
	   gem 'guard-rspec', '~> 4.7', '>= 4.7.2' #guard和rspec结合的第三方插件(可以帮你配置好Guardfile文件)
	end
        # [guard plugin](https://github.com/guard/guard/wiki/Guard-Plugins)
         guard init rspec  #初始化guardfile文件(这玩意儿我自己还不知道咋写)
       bundle exec guard  #一旦有文件变动会自动运行测试(其实就是在运行在guardfile里面配置的一条命令)