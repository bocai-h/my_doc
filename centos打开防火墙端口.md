# centos7防火墙操作

打开8000端口
~~~~
iptables -I INPUT -p tcp --dport 8000 -j ACCEPT

~~~~

关闭防火墙服务

~~~~
systemctl stop firewalld.service搜索 #停止
systemctl disable firewalld.service #禁用

~~~~
