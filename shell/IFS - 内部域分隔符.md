# IFS
IFS是shell脚本的内置变量，全称为 内部域分隔符（Internal Field Seprator）  
其作用是用于拆解读入的数据
默认情况下，“空格”/“tab”/“\n”均为IFS  
这也就说明了IFS可以支持同时设置多个值

## example
例如文本内容如下：
a b  
a,b  
当使用默认IFS读入时，文本会因为空格而输出三行：
> for line in `cat example.txt`; do  
>   echo $line  
> done  


## change IFS
当需要对IFS进行控制时，可以使用如下方法（只对换行符敏感）  
> oldifs=\$IFS  
IFS="\n"  
（do shell ...）  
IFS=$oldifs  

这里需要注意，为了保证其他shell命令工作正常，再修改IFS后需要对其进行还原