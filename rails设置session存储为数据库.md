# Rails中session设置过期

config/initializers/session_store.rb:中设置为数据库存储模式

````
Foo::Application.config.session_store :active_record_store {:key => 'depot', :secret => '5xb5x1g92e965b95b16e49x79gxx9999', :expire_after => 1.years}

````

key名称
secret安全码
expire_after过期时间