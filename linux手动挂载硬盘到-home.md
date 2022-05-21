title: linux手动挂载硬盘到/home
categories: 教程
tags: [linux,硬盘挂载]
date: 2021-08-21 12:19:00
---
0、创建挂载目录

mkdir -p /home
1、确认是否有没有分区的磁盘,分区的磁盘是 /dev/vdb ,在您的服务器中可能是 /dev/vdb 请注意按实际名称修改

fdisk -l

2、为磁盘分区，若已分区的，请跳过！
fdisk /dev/vdb

3、输入n开始创建分区

4、输入p创建主分区

5、选择分区号，这里输入1

6、输入分区开始位置，直接回车

7、输入分区结束位置，直接回车

8、输入wq 保存退出

9、检查是否分区成功

fdisk -l

10、格式化分区，这里请输入你看到的磁盘加分区号，如下图，已格式化过的，请跳过
mkfs.ext4 /dev/vdb

11、将分区挂载信息添加到开启动挂载

echo "/dev/vdb /home ext4 defaults 0 0" >> /etc/fstab


12、重新挂载所有分区

mount -a


13、检查是否挂载成功

df -h