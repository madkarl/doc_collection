# df
查看磁盘用量

## params
-a:  
显示全部磁盘分区（包含伪磁盘） 
-h:  
显示人类可读的磁盘大小

## example
[ctu@ctu-clouds-01 var]$ df -ah  
Filesystem      Size  Used Avail Use% Mounted on  
/dev/vda1        50G  2.5G   45G   6% /  
proc               0     0     0    - /proc  
sysfs              0     0     0    - /sys  
devpts             0     0     0    - /dev/pts  
/dev/vdb1        92G   67M   87G   1% /tmp  
/dev/vdb2       2.8T   47G  2.7T   2% /home  
none               0     0     0    - /proc/sys/fs/binfmt_misc  
