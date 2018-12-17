# date
date用于获取格式化的时间和日期

> $ date  
> Tue Dec 11 16:01:43 CST 2018  

## usage
date [OPTION]... [+FORMAT]

## params
name|comment
--|--
-d| 日期格式字符串

## example
获取指定格式的前一天日期
> $ date -d "1 day ago" +"%Y%m%d"  
> 20181210

获取指定格式的日期
> $ date  +"%Y%m%d"  
> 20181211
