# Mysql 备份


## 主从备份
以HiveMetastore做HA时同步HIVE数据库为例

### Step 1: 数据同步
#### 空数据库同步
如果是对新库进行备份只需要在主从两侧建立好同名数据库即可
#### 有数据的数据库同步
锁库-导出-开锁-导入

### Step 2: 修改配置文件
/etc/my.cnf  
#### 主节点
添加&修改内容如下
**************************
[mysqld]  
server-id=1  
log-bin = mysql-bin  
binlog_format = mixed  
log_slave_updates=ON
  
binlog-do-db = hive  
binlog-ignore-db = mysql  
binlog-ignore-db = information_schema  
binlog-ignore-db = performance_schema  
**************************
server-id  每个节点保持编号不同即可  
binlog-ignore-db 热备中需要忽略的库  
binlog-do-db 热备中需要备份的数据库  

#### 从节点
添加&修改内容如下
**************************
[mysqld]  
server-id=2  
relay_log = mysqld-relay-bin
log-slave-updates = ON
  
replicate-do-db = hive
replicate-ignore-db = mysql
replicate-ignore-db = information_schema
replicate-ignore-db = performance_schema

************************** 
relay_log 表示将从主节点上读取数据写入自身
log-slave-updates 保证同步来的数据可以更新到自身的从节点
auto_increment_offset 自增记录从1开始  
auto_increment_increment 自增ID每次+2（避免主主模式下同时插入导致ID重复）  
replicate-ignore-db 热备中需要忽略的库  
replicate-do-db 热备中需要备份的数据库  

### Step 3: 记录主库信息
> mysql> show master status\G  

得到如下内容：  
File: mysql-bin.000006  
Position: 120

### Step 4: 从节点设置
> $ mysql -uroot -p  
> mysql> CHANGE MASTER TO MASTER_HOST='xxx', MASTER_USER='username', MASTER_PASSWORD='password', MASTER_LOG_FILE='mysql-bin.000006', MASTER_LOG_POS=120;  

MASTER_HOST = 主节点HOSTNAME或IP
MASTER_USER = 主节点上有备份权限的mysql账号
MASTER_PASSWORD = MASTER_USER对应的密码
MASTER_LOG_FILE = Step 3 中File数值
MASTER_LOG_POS = Step 3 中Position数值

### Step 5: 检查备份状态
> mysql> show slave status\G  

检查以下内容：  
 Slave_IO_Running: Yes  
 Slave_SQL_Running: Yes  
 如果有任意一项不是Yes则需要查看/var/log/mysqld.log进行排错

## 主主备份
主主备份就是在主从备份的基础上，反向进行一次主从备份即可