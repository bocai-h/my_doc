# Rails5增加的一些命令

~~~~
rails -T

~~~~

即可查看


~~~~
  #清空日志
   rails log clear
 
  #输出middleware栈
    rails middleware

  
 #输出当前的schema版本号
   rails db:version

 #Dumps the database structure to db/structure.sql
  rails db:structure:dump

 #Recreates the databases from the structure.sql file
 rails db:structure:load

 #Drops the database from DATABASE_URL or config/database.yml 
  rails db:drop

 # Creates the database from DATABASE_URL or config/database.yml for the current RAILS_ENV

 rails db:create

 #Remove old compiled assets
 rails assets:clean
~~~~