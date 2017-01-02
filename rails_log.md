# rails日志

rails日志存在于app/log下面.对于不同环境的日志内容会有差别.development下会把每次对数据库的访问代码包含进去,production会省略,不过也会有很多的内容

- environment.rb
~~~~
 config.log_level = :debug

~~~~

- production.rb 希望输出少量的日志

~~~~
  config.log_level = :warn

~~~~

## log level介绍

Rails可以通过不同的log_leve来控制文件的输出
> 1. :debug      
   2. :info
   3. :warn
  4. :error
  5. :fatal


1. :debug level提供最详细的log,可以将每一条sql都记录下来
2. :infolevel是production环境下的默认设置,不会写出sql的执行情况,但也会很详细,如果是ActiveMailer,它会记录下每封信的内容,Log文件内容就是快速增长
3. :warn level等log level只记录重要的信息


## 日志过多清除日志

利用rails本身提供的task即可

~~~~
  rake log:clear

~~~~

