# centos包管理器(yum)总结

yum check-update  查看可以更新的软件包
yum update 更新所有的软件包
yum update kernel 更新指定的软件包
yum upgrade 大规模更新升级

rpm包的安装和删除

yum install xxx(服务名)  安装rpm包
yum remove xxx(服务名) 删除rpm包

yum缓存信息

yum clean packages 清除缓存的rpm包文件
yum clean headers  清除缓存的rpm头文件
yum clean older headers 清除缓存中旧的头文件
yum clean all 清除缓存中旧的rpm头文件

文件

查询软件包信息

yum list 列出资源库中所有可以安装或更新的rpm包

yum list firefox* 
yum list update 列出资源库中可以更新的rpm包
yum list installed
yum list extras 列出已安装但不包含在资源库中的rpm包

yum info firefox* 列出资源库中可以更新的rpm包信息 
yum info update
yum info installed
yum info extras

yum search firefox 搜索匹配特定字符的rpm包
yum provides firefox 搜索包含特定文件的rpm包