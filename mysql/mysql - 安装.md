# Mysql Install Doc

## Step 0: remove old mysql compants and maria db
> $ yum remove mysql* mariadb*  

## Step 1: download repos
### Centos 6
> $ wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm  
> $ yum local install mysql-community-release-el6-5.noarch.rpm  

### Centos 7
> $ wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm  
> $ yum local install mysql-community-release-el7-5.noarch.rpm  

## Step 2: install from yum
> $ yum install mysql-community-server

## Step 3: move mysql data dir
### /etc/my.cnf
> $ cp -R -p /var/lib/mysql /data/mysql
> $ rm -rf /var/lib/mysql/*
> $ vim /etc/my/cnf  
modify "dataDir=/var/lib/mysql" to other data dir  
such as:  
dataDir=/data/mysql  

### /ect/init.d/mysqld
this only for Centos 6
> $ vim /etc/init.d/mysqld
modify "dataDir=/var/lib/mysql" to the same value with /etc/my.cnf seted.

# Step 4: startup service
Centos 6:  
> $ service mysqld start  
Centos 7:  
> $ systemctl mysqld start  

## Step 5: basic security setting
> $ /usr/bin/mysql_secure_installation

## Step 6: test connection
> $ mysql -uroot -p  
> mysql> show databases;  



