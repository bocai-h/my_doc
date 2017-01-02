# linux常用命令总结

- ls-lht
> l 列表形式显示 t按时间排序  h按人类好识别的方式显示出来 列表形式显示出来会同时显示文件或文件夹的大小

- du -sh *
> * 代表文件或者文件夹 h代表人类好识别的方式(文件大小有单位)

- tracepath host_path
> tracepath追踪出到指定的目的地址的网络路径，并给出在路径上的每一跳（hop）。如果你的网络有问题或是慢了，tracepath可以查出网络在哪里断了或是慢了。

- mtr host_path
> mtr命令把ping命令和tracepath命令合成了一个。mtr会持续发包，并显示每一跳ping所用的时间。也会显示过程中的任何问题

- nano -c 文件
> 这种模式下打开的nano会显示行数



