# sort
根据指定列进行排序

## example
根据第二列进行排序，列使用“ ”进行分割  
[ctu@ctu-clouds-01 test]$ cat test.txt  
banana 12  
apple 1  
orange 8  
[ctu@ctu-clouds-01 test]$ sort -t " " -k 2 test.txt  
apple 1  
banana 12  
orange 8  
