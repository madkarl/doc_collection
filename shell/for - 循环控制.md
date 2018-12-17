# for
在shell中有两种for循环的写法

## type-1
> for x in y; do  
> ...  
> done  

### example
遍历全部参数
> for arg in $@; do  
> 	echo $arg  
> done  


## type-2
> for ((x=y;x<z;x++>))  
> {  
> ...  
> }  

### example
遍历从当前开始的前N天
> for((x=0;x<10;x++))  
> {
> 	dt=\`date -d "$x day ago" +"%Y-%m-%d"\`  
> 	echo $dt  
> }  
