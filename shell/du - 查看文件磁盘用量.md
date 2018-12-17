# du
查看目录及文件占用磁盘大小

## params
-a:  
查询全部文件，不加此参数则只查询目录大小  
-h:  
显示人类可读的文件大小信息  
--max-depth=N:  
最多显示几层目录  

## example
[ctu@ctu-clouds-01 ~]$ du -h --max-depth=1 /home/ctu  
8.0K    /home/ctu/.vim  
64K     /home/ctu/tools  
24K     /home/ctu/.local  
8.0K    /home/ctu/.oracle_jre_usage  
4.0K    /home/ctu/.idlerc  
16K     /home/ctu/data  
763M    /home/ctu/resource  
45G     /home/ctu/clouds  
1.3M    /home/ctu/.cache  
403M    /home/ctu/soft  
32K     /home/ctu/.ssh  
8.0K    /home/ctu/.pki  
4.0K    /home/ctu/.beeline  
182M    /home/ctu/build  
47G     /home/ctu  