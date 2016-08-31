# Rails::Railtie

Rails::Railtie是Rails框架的核心,它提供很多的钩子(hooks)去扩展Rails或者说去修改初始化流程

Rails的每个主要组件(Action Mailer,Action Controller,Active Record,etc)都实现了railtie.它们各自负责自己的初始化.这种方式可以让Rails和这些组件的耦合最小化,也就可以根据自己的需要去替换Rails的这些默认组件了.(充分的提供了灵活性)

