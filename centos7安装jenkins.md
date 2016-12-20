# centos7上配置jenkins

- 配置java环境
> 下载jdk,设置环境变量
- 安装tomcat
> 到官网下载稳定版本的tomcat,解压,进步bin目录启动tomcat

- 到浏览器中输入localhost:8080
> 如果此时呈现出tomcat的界面则证明tomcat没问题了

- 到jenkins官网下载对应操作系统的jenkins.war
> 将jenkins.war移动到tomcat的webapps下,从新启动tomcat

- 在浏览器中输入localhost:8080/jenkins即会呈现出jenkins的界面
> 会提示你到服务器中拿到jenkins的密码就可以进入安装插件了

- 对jenkins进行配置

 [jenkins配置手册](http://files.cnblogs.com/files/zz0412/jenkins%E5%85%A5%E9%97%A8%E6%89%8B%E5%86%8C.pdf)
