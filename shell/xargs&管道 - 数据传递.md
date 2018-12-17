# xargs & pipe
当多条命令需要对数据进行传递时，需要使用管道或者xargs

## pipe
在linux shell中，使用“|”表示管道  
其意义为：“|”前命令的标准输出作为“|”后命令的标准输入

### attention
管道后面的命令必须支持标准输入，如cat/head/tail等命令

### example
如test.txt共存在三行，使用cat对其进行输出，并将结果输出到管道中，最后使用head查看其前两行  
[ctu@ctu-clouds-01 ~]$ cat test.txt   
1  
2  
3  
[ctu@ctu-clouds-01 ~]$ cat test.txt | head -2  
1  
2  

## xargs
此命令可以从标准输入中构建并执行命令
当管道后面的命令不支持标准输入时，需要使用xargs加pipe的组合来实现

### example
由于ls不支持标准输入，故此行命令使用xargs来接收管道的输出，并将其拼接到"ls -l"后面，形成可执行的“ls -l /”命令  
[ctu@ctu-clouds-01 ~]$ echo "/" | xargs ls -l  
total 88  
dr-xr-xr-x.   2 root root  4096 Nov  3 16:22 bin  
dr-xr-xr-x.   4 root root  4096 Aug 27 12:09 boot  
drwxr-xr-x.   2 root root  4096 Dec 25  2014 data  
drwxr-xr-x   17 root root  3540 Nov 28 16:17 dev  
drwxr-xr-x.  72 root root  4096 Dec  2 13:37 etc  
drwxr-xr-x    3 root root  4096 Nov  7 15:20 home  
...