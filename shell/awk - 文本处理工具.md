# awk
其原理是对输入的文件进行逐行读入，并且根据分隔符进行切片，再对每一片进行处理  
awk支持自定义分隔符，正则表达式，数组，内置变量和函数，以及流程控制语句


## usage
> awk -F 'sep' '{function}' file


## params
name|comment
--|--
-F| 指定分隔符
-v| 添加变量

## inner function
name|comment
--|--
NR| 当前行数
NF| 当前行分片数 

## inner params
name|comment
--|--
print| 打印
split| 分割
substr| 子字符串 

## examples
### 从passwd文件中查找所有用户名
[k@k00 ~]$ awk -F ':' '{print $1}' /etc/passwd  
root  
bin  
daemon  
adm  
...

### 获取passwd中账号和shell，并在开头加上head，结尾加上"test,/bin/bash"
[k@k00 ~]$ awk -F ':' 'BEGIN{print "name\tshell"}{print $1"\t"$7}END{print "blue\t/bin/bash"}' /etc/passwd  
name    shell  
root    /bin/bash  
bin     /sbin/nologin  
...  
blue    /bin/bash

### 搜索passwd中所有带root的行
[k@k00 ~]$ awk -F':' '/root/{print $0}' /etc/passwd   
root:x:0:0:root:/root:/bin/bash  
operator:x:11:0:operator:/root:/sbin/nologin  

### 显示passwd文件每行行号，分片数和账号
[k@k00 ~]$ awk -F':' '{print NR"\t"NF"\t"$0}' /etc/passwd  
1       7       root:x:0:0:root:/root:/bin/bash  
2       7       bin:x:1:1:bin:/bin:/sbin/nologin  
3       7       daemon:x:2:2:daemon:/sbin:/sbin/nologin  
4       7       adm:x:3:4:adm:/var/adm:/sbin/nologin  

### 统计文本中所有人一月份的收入综合
(0=manager, 1=worker)
Tom	 0   2012-12-11      car     3000  
John	 1   2013-01-13      bike    1000  
vivi	 1   2013-01-18      car     2800  
Tom	 0   2013-01-20      car     2500  
John	 1   2013-01-28      bike    3500  
### 命令行执行
因为文件中的分隔符空格是默认分隔符，故分隔符参数可以忽略  
[k@k00 ~]$ awk '{split($3,dt,"-");if(dt[2]=="01"){ret[$1]+=$5};if($2=="1"){job[$1]="worker"}else{job[$1]="manager"}}END{for(r in ret){print r"\t"job[r]"\t"ret[r]}}' test.txt  
vivi    worker  2800  
Tom     manager 2500  
John    worker  4500  

### 读文件执行
将匿名函数的内容写入到文件中(vim test_func):  
> {split($3,dt,"-");if(dt[2]=="01"){ret[\$1]+=$5};if($2="1"){job[$1]="worker"}else{job[$1]="manager"}}END{for(r in ret){print r"\t"job[r]"\t"ret[r]}}   

如果要对文件进行个格式化，左大括号不能单独起一个新行  
[k@k00 ~]$ awk -F ' ' -f test_func test.txt   
vivi    worker  2800  
Tom     manager 2500  
John    worker  4500  

### 将shell变量赋值给awk使用
如果是作为普通的awk参数，变量可以直接使用
用过变量需要用于awk函数逻辑，则需要进行注册
> username="root"  
> echo \`awk -v user=$username -F':' '{if(user==$1){print $0}}' /etc/passwd\`