# cut
切割文件，并显示指定列

## params
name|comment
--|--
-f| 选择显示的列
-s| 不现实没有分隔符的列
-d| 指定分隔符

## example
将文件每一行按" "来分割，取其前两列  
[ctu@ctu-clouds-01 test]$ cat test.txt   
0  
1 a aa  
2 b bb bbb  
3 c cc ccc cccc  
[ctu@ctu-clouds-01 test]$ cut -d ' ' -f 1,2 -s test.txt  
1 a  
2 b  
3 c  