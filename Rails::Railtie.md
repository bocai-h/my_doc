# Rails::Railtie

Rails::Railtie是Rails框架的核心,它提供很多的钩子(hooks)去扩展Rails或者说去修改初始化流程

Rails的每个主要组件(Action Mailer,Action Controller,Active Record,etc)都实现了railtie.它们各自负责自己的初始化.这种方式可以让Rails和这些组件的耦合最小化,也就可以根据自己的需要去替换Rails的这些默认组件了.(充分的提供了灵活性)

发一个Rails扩展不需要实现一个railtie,但是如果你需要与rails框架在启动中或者启动后进行交互,railstie就是需要的

比如: 你的扩展需要做如下的事情就需要railtie

 . creating initializers
 . configuring a Rails framework for the application,like setting a generator
. adding config.* keys to the environment
.setting up a subscriber with ActiveSupport::Notifications
.adding Rake tasks 