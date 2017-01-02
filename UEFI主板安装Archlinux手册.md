# UEFI主板Archlinux安装

*经过几天的奋战，总算在UEFI主板的机器上把Archlinux装上了，不容易，特写此文，一来为了给自己做笔记，二来希望能帮助下看到本文的有缘人。愿大家在Archlinux这条路上走的更远*

1.到archlinux官网下载最新的archlinux镜像,通过dd命令制作启动u盘
 > lsblk查看当前u盘在文件系统的名字,一般插入u盘后系统会为u盘命名为/dev/sdb

~~~~
   # cd到镜像所在文件夹下 bs为输入输出的速度
   dd if=archlinux.iso of=/dev/sdb bs=1M

~~~~
2.分区(使用parted 不要使用fdisk)
> - sblk 查看当前硬盘名称(一般为/dev/sda)
> - 利用parted工具分盘
   parted /dev/sda(进入parted模式)
         mklabel gpt 建立分区表
         mkpart ESP fat32 1MiB 513MiB 引导区
         set 1 boot on
         mkpart primary linux-swap 513MiB 4.5GiB 分4G作为swap虚拟内存
         mkpart primary ext4 4.5GiB 100% root目录
         q退出保存  help输出帮助命令（parted模式下）


3.格式化分区
> mkfs.fat -F32 /dev/sda1 启动区应该格式化为fat格式
   mkswap /dev/sda2 swap分区格式化为swap格式
   swapon /dev/sda2  开启虚拟内存
   mkfs.ext4 /dev/sda3 root目录格式化为ext4格式

4.挂载分区
> mkdir -p /mnt/boot 创建boot文件夹
   mount /dev/sda3 /mnt/ 把根目录挂载到mnt/目录下
   mount /dev/sda1 /mnt/boot 把启动区挂载到/mnt/boot/目录下

5.安装基础包
~~~~
pacstrap -i /mnt base base-devel

~~~~
6.生成fstab文件
~~~~
genfstab -U /mnt > /mnt/etc/fstab

~~~~
7. wifi-menu连接wifi

8.进入硬盘系统
~~~~
arch-chroot /mnt /bin/bash #前提是基础包安装成功

~~~~

.生成引导区

~~~~
bootctl install #会在/boot下生成EFI和loader文件夹
#创建/boot/loader/entries/arch.conf文件写入内容

title          Arch Linux
linux          vmlinuz-linux
initrd         initramfs-linux.img
options      root=/dev/sda3 rw

# root这里写的是你的root目录
# 修改/boot/loader/loader.conf
timeout 3
default arch

# 生成引导区的时候必须保证安装基础包时在boot目录下有vmlinuz-linux和initramfs-linux.img文件

~~~~

9.安装NetworkManager(在连接wifi成功的情况下一定要先装,有时候wifi总是连不上)

~~~~
pacman -Syu networkmanager

~~~~

10.设置开机启动NetworkManager(也可以重新硬盘启动后运行)

~~~~
  systemctl enable NetworkManager

# 立即启动 NetworkManager

 systemctl start NetworkManager

# 查看系统中有哪些服务正在运行
 
systemctl --type=service 

#你必须确保没有其他想要配置网络相关的服务正在运行; 事实上, 多个网络配置服务之间会相互冲突

~~~~

11.安装kde5
~~~~
#安装plasma
pacman -S plasma
#安装sddm  sddm是KDE Plasma桌面环境首选的显示管理器
pacman -S sddm 
#设置sddm开机启动
systemctl enable sddm

~~~~

12.安装yaourt
~~~~
#最简单安装Yaourt的方式是添加Yaourt源至您的 /etc/pacman.conf:
[archlinuxcn]
#The Chinese Arch Linux communities packages.
SigLevel = Optional TrustAll
Server   = http://repo.archlinuxcn.org/$arch
#同步并安装：
pacman -Syu yaourt

~~~~
13.退出U盘系统，重新启动（从硬盘）

14.配置字符集
~~~~
  nano /etc/locale.gen
 
 en_US.UTF-8
 zh_TW.UTF-8
 zh_HK.UTF-8
 zh_CN.UTF-8
 zh_CN.GBK
 zh_CN.GB2312

#执行locale-gen以生成locale讯息
 locale-gen
echo LANG=en_US.UTF-8 > /etc/locale.conf
 
~~~~
15.关于镜像(设置好的镜像列表可以加快下载速度,可以在前面的步骤进行)
~~~~
 # 进入硬盘系统中
 cd /etc/pacman.d/
  mv mirrorlist mirrorlist.bk
 wget http://www.catsoft.me/mirrorlist

~~~~

17.设置时区
~~~~
 ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
# 硬件时间 在计算机所有操作系统上统一硬件时间模式，否则可能会发生冲突 可以用下面命令自动生成/etc/adjtime
# UTC（推荐）
hwclock --systohc --utc

~~~~

18.设置主机名
~~~~
 echo hostname > /etc/hostname
 nano /etc/hosts 
 #写到127后   
 127.0.0.1 localhost hostname

~~~~

19.设置root密码（此时只有root账户）
~~~~
passwd root

~~~~
20.添加用户
~~~~
 useradd -m username
 passwd username 

~~~~