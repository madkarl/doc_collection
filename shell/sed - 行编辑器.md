# sed
用于过滤和转换字符串的流处理工具

- [sed](#sed)  
    - [usage](#usage)  
    - [params for option](#params-for-option)  
    - [parmas for command](#parmas-for-command)  
    - [params for address](#params-for-address)  
    - [examples](#examples)  
            - [删除一行，并且存回原文件](#删除一行并且存回原文件)  
            - [在第二行后面追加一行](#在第二行后面追加一行)  
            - [将每行中所有的test替换为hello](#将每行中所有的test替换为hello)  
            - [删除带有指定内容的行](#删除带有指定内容的行)  

## usage
sed [option] "address command" file_path

## params for option
name|comment
--|--
-n| 静默模式，不显示原来默认模式的内容
-i| 直接修改原文件
-e| 执行脚本
-f| 指定脚本位置
-r| 使用正则表达式的扩展内容

## parmas for command
name|comment
--|--
d| 删除符合条件的行
p| 显示符合条件的行
a\string| 在指定内容后面追加新行,string为新行内容
i\string| 在指定内容行的前面追加新行,string为新行内容
r FILE| 将制定的文件内容添加到符合条件处
w FILE| 将制定范围内容写入到指定文件中
s/partten/string/ext_opt| 查找并替换，默认只替换第一次匹配到的内容
g| 行内替换所有内容
i| 替换时忽略大小写

## params for address
指定sed搜索范围

## examples
#### 删除一行，并且存回原文件  
[ctu@ctu-clouds-01 test]$ cat test.txt   
banana 12  
apple 1  
orange 8  
[ctu@ctu-clouds-01 test]$ sed -i "3d" test.txt  
[ctu@ctu-clouds-01 test]$ cat test.txt  
banana 12  
apple 1  
#### 在第二行后面追加一行  
[ctu@ctu-clouds-01 test]$ sed -i "2a\test" test.txt  
[ctu@ctu-clouds-01 test]$ cat test.txt  
banana 12  
apple 1  
test  
#### 将每行中所有的test替换为hello  
[ctu@ctu-clouds-01 test]$ cat test.txt  
banana 12  
test test  
apple 1  
test  
[ctu@ctu-clouds-01 test]$ sed "s/test/hello/g" test.txt  
banana 12  
hello hello  
apple 1  
hello  
#### 删除带有指定内容的行  
[ctu@ctu-clouds-01 test]$ cat test.txt  
banana 12  
test test  
apple 1  
test  
[ctu@ctu-clouds-01 test]$ sed "/test/d" test.txt  
banana 12  
apple 1  
#### 替换inittab中的默认启动方式
inittab中有一行内容如下： 
id:3:initdefault:  
如果想将其中的3替换为8，可以使用下面的命令
[ctu@ctu-clouds-01 test]$ sed -r "s/([id:])[0-9](:initdefault:)/\18\2/" /etc/inittab  
或者  
[ctu@ctu-clouds-01 test]$ sed "s/\([id:]\)[0-9]\(:initdefault:\)/\18\2/" /etc/inittab  
其中  
-r 表示正则扩展  
([id:])和(:initdefault:)表示该模式匹配的前后内容  
\1和\2 表示正则中的反向引用，即前面的第一段和第二段