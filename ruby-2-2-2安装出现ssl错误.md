# rvm安装ruby 2.2.2 openssl出错

正确的方式

~~~~
rvm install 2.2.2 --with-openssl-dir=$HOME/.rvm/usr  --with-readline

~~~~

参考帖子为openssl打补丁也行
[github帖子](https://github.com/rvm/rvm/issues/3548)