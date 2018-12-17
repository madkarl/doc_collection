# Mysql Optimize doc

## [mysqld]
key|value|comment
--|--|--
max_connections|100|最大连接数,提高并发,内存开销与实时并发链接数量正相关
innodb_file_per_table|1|每个表具有自己独立的表空间和独立文件,drop table自动回收空间
innodb_flush_log_at_trx_commit|2|
innodb_log_buffer_size|64M|
innodb_buffer_pool_size|1G|
innodb_thread_concurrency|8|
innodb_flush_method|O_DIRECT|
innodb_log_file_size|512M|