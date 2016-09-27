# linux中格式化U盘

- 格式化为fat32
~~~~
 sudo mkfs.vfat -F 32 /dev/sdb1
 
~~~~

- 格式化为ntfs

~~~~
 sudo mkfs.ntfs -L NTFS /dev/sdb1
 
~~~~