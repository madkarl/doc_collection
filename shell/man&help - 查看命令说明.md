# man&help
查询各命令的使用方法

## man
查看外部命令的使用方法  

### usage
> man \<type\> command  
当在不同类型下存在同名命令时，需要指定类型编号
type:  
 1. 用户命令(/bin,/usr/bin,/usr/local/bin)
 2. 系统调用(c-api)
 3. 库用户
 4. 特殊文件/设备文件
 5. 文件格式(配置文件语法)
 6. 游戏
 7. 杂项
 8. 管理命令(/sbin,/usr/sbin,/usr/local/sbin)

### install
当系统中没有man组件时，需要进行安装
> yum install man man-pages

### example
[ctu@ctu-clouds-01 ~]$ man ifconfig  
IFCONFIG(8)                Linux Programmer’s Manual               IFCONFIG(8)  
NAME  
       ifconfig - configure a network interface  
SYNOPSIS  
       ifconfig [interface]  
       ifconfig interface [aftype] options | address ...  
...  

[ctu@ctu-clouds-01 ~]$ man 2 read  
READ(2)                    Linux Programmer’s Manual                   READ(2)  
NAME  
       read - read from a file descriptor  
...  

## help
查看内部命令的使用方法

## example
[ctu@ctu-clouds-01 ~]$ help cd  
cd: cd [-L|-P] [dir]  
    Change the shell working directory.  
...
