# wc
查看文件统计信息（行数/字节数）

## params
name|comment
--|--
-c| 读取字节数
-l| 读取行数

## example
[ctu@ctu-clouds-01 test]$  wc -l test.txt  
3 test.txt  
[ctu@ctu-clouds-01 test]$ cat test.txt |wc -l  
3  