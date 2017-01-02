# Aria2c下载工具使用

[原文地址](http://sydi.org/posts/linux/aria2c-usage-sample-cns.html)
原文中有更多的高级功能

- 基本使用
 
下载一个文件
~~~~
# 1.10.0版本后对每个host使用1个链接
aria2c http://host/image.iso

#你可以使用-max-connection-per-server或者-x选项进行改变

~~~~

用每个host两个连接从一个host下载一个文件

~~~~
 aria2c -x2 http://host/image.iso
~~~~
说明:想要停止下载,可以按Ctrl-C.想要恢复下载,可以在同一个文件夹中执行相同的下载命令.只要URI指向同一个文件,URIs是可以被改变的.

同时使用两个连接下载同一文件

~~~~
aria2c -s2 http://host/image.iso http://mirror1/image.iso http://mirror2/image.iso

~~~~
说明:你可以指定URIs的数量多于-s选项设定的数.在这个例子中,前两个URL会被用于下载,而第三个URL作为备用(如果前面两个有个挂了,第三个顶上)

同时从FTP和HTTP源下载一个文件

~~~~
aria2c http://host1/file.zip ftp://host2/file.zip

~~~~

并行下载任意数目的URI,metalink,torrent

~~~~
aria2c -Z http://host/file1 file2.torrent file3.metalink

~~~~

说明: 如果你只是下载torrent和metalink的文件,那么选项-Z将不是必须的.所以你可以使用以下这个命令同时下载bt文件

~~~~
aria2c file1.torrent file2.torrent

~~~~

并发下载一个文件的URI

~~~~
aria2c -ifiles.txt -j5
~~~~
说明:选项-j用于指定同时下载的文件的数量.你可以在文件中指定bending的torrent和metalink文件
说明:你可以指定一些选项在下载文件中
在退出时保存错误/未完成的下载

~~~~
aria2c -ifiles.txt --save-session=out.txt
~~~~
当你按下Ctrl-C或者aria2退出时,所有的错误(error)/未完成(unfinished)下载将会保存到out.txt文件中.注意通过XML-RPC方式添加的下载不会被保存!你可以使用这个文件作为一个输入文件列表(input file list)来重新开始下载

~~~~
aria2c -iout.txt
~~~~

BT下载(BitTorrent Download)
通过网上的种子文件下载

~~~~
aria2c http://site/file.torrent
~~~~

通过网上的种子文件下载,种子保存在内存

~~~~
aria2c --follow-torrent=mem http://site/file.torrent
~~~~

通过本地的种子文件下载
~~~~
aria2c -u40k /path/to/file.torrent

~~~~
说明: -u,-max-upload-limit指定最大的上传速度
说明: 想要停止下载可以按Ctrl-C.想要恢复下载,可以在同一个文件夹中执行相同的下载命令.只要URI指向同一个文件,URIs是可以被改变的

通过bt magnet uri下载

~~~~
aria2c "magnet:?xt=urn:btih:248D0A1CD08284299DE78D5C1ED359BB46717D8C&dn=aria2"

~~~~
说明: 在bt magnet uri包含"&"的时候记住尧家单引号或者双引号.强烈推荐打开DHT选项

保存元数据到.torrent文件中

~~~~
 aria2c --bt-save-metadata "magnet:?xt=urn:btih:248D0A1CD08284299DE78D5C1ED359BB46717D8C&dn=aria2"
~~~~
上面那个命令会保存元数据到一个名为"248d0a1cd08284299de78d5c1ed359bb46717d8c.torrent"的种子文件

自动调节连接数
如果每个种子的下载速度都低于200k的话,按日aria2会临时增加连接数来试着提高下载速度

~~~~
aria2c --bt-request-peer-speed-limit=200k file.torrent
~~~~
说明: 配置-bt-request-peer-speed-limit选项为合适的值可以在某些情况下提高你的下载速度