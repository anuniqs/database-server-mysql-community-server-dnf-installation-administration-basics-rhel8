## Install MySQL community server - 

### Step 1 — Installing MySQL

[root@192 ~]# sudo dnf install mysql-server

**Default Port 3306**

[root@192 ~]# rpm -qi mysql

[root@192 ~]# sudo systemctl start mysqld.service
[root@192 ~]# sudo systemctl status mysqld.service

[root@192 ~]# sudo systemctl enable mysqld.service


### Step 2 — Securing MySQL

[root@192 ~]# sudo mysql_secure_installation

```
Please set the password for root here.


New password: 

Re-enter new password: 
```

### Step 3 — Testing MySQL

[root@192 ~]# mysqladmin -u root -p version

```
Enter password:
mysqladmin  Ver 8.0.21 for Linux on x86_64 (Source distribution)
Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Server version          8.0.21
Protocol version        10
Connection              Localhost via UNIX socket
UNIX socket             /var/lib/mysql/mysql.sock
Uptime:                 8 min 13 sec

Threads: 2  Questions: 13  Slow queries: 0  Opens: 131  Flush tables: 3  Open tables: 49  Queries per second avg: 0.026
```

[root@192 ~]# mysql -u root -p


## MySQL Admin - 

### Set MySQL Root password

[root@192 ~]# mysqladmin -u root password @password


### Change MySQL Root password

[root@192 ~]# mysqladmin -u root -p@password password '@20Password'

[root@192 ~]# mysqladmin -u root -p version (Use new password)


### Check MySQL Server is running

[root@192 ~]# mysqladmin -u root -p ping

```
Enter password:
mysqld is alive
```

### Check status of all MySQL Server Variable’s and value’s

[root@192 ~]# mysqladmin -u root -p extended-status


### check all the running Process of MySQL server

[root@192 ~]# mysqladmin -u root -p processlist


### Create a Database in MySQL server

[root@192 ~]# mysqladmin -u root -p create database_name

[root@192 ~]# mysql -u root -p

mysql> show databases;


### Drop a Database in MySQL server

[root@192 ~]# mysqladmin -u root -p drop database_name


### reload/refresh MySQL Privileges

[root@192 ~]# mysqladmin -u root -p reload;

[root@192 ~]# mysqladmin -u root -p refresh;


### MySQL Flush commands

[root@192 ~]# mysqladmin -u root -p flush-hosts

```
flush-hosts: Flush all host information from host cache.
flush-tables: Flush all tables.
flush-threads: Flush all threads cache.
flush-logs: Flush all information logs.
flush-privileges: Reload the grant tables (same as reload).
flush-status: Clear status variables.
```

### Connect remote mysql server

[root@192 ~]# telnet localhost 3306

[root@192 ~]# telnet ip_address 3306


[root@192 ~]# mysqladmin -h 192.168.43.135 -u root -p status

```
error: 'Access denied for user 'root'@'192.168.43.135' (using password: YES)'
```

[root@192 ~]# mysqladmin -h 192.168.43.135 -u user_name -p status

```
error: 'Host '192.168.43.135' is not allowed to connect to this MySQL server'
```

[root@192 ~]# mysql -u root -p

mysql> CREATE USER 'user_name'@'localhost' IDENTIFIED BY '@20Password';

mysql> GRANT ALL PRIVILEGES ON *.* TO 'user_name'@'localhost' WITH GRANT OPTION;

mysql> CREATE USER 'user_name'@'%' IDENTIFIED BY '@20Password';

mysql> GRANT ALL PRIVILEGES ON *.* TO 'user_name'@'%' WITH GRANT OPTION;

mysql> FLUSH PRIVILEGES;


[root@192 ~]# mysqladmin -h 192.168.43.135 -u user_name -p status

```
Enter password:

Uptime: 4409  Threads: 2  Questions: 62  Slow queries: 0  Opens: 217  Flush tables: 3  Open tables: 135  Queries per second avg: 0.014
```


## Grant Different User Permissions - 

### List of user 

mysql> SELECT user FROM mysql.user;

mysql> SELECT user,host FROM mysql.user;


### Create a user

mysql> CREATE USER 'new_user'@'localhost' IDENTIFIED BY '@20Password';

mysql> SELECT user,host FROM mysql.user;

mysql> GRANT ALL PRIVILEGES ON * . * TO 'new_user'@'localhost';

mysql> FLUSH PRIVILEGES;

```
ALL PRIVILEGES- as we saw previously, this would allow a MySQL user full access to a designated database (or if no database is selected, global access across the system)

CREATE- allows them to create new tables or databases

DROP- allows them to them to delete tables or databases

DELETE- allows them to delete rows from tables

INSERT- allows them to insert rows into tables

SELECT- allows them to use the SELECT command to read through databases

UPDATE- allow them to update table rows

GRANT OPTION- allows them to grant or remove other users’ privileges
```

mysql> GRANT type_of_permission ON database_name.table_name TO 'username'@'localhost';

mysql> REVOKE type_of_permission ON database_name.table_name FROM 'username'@'localhost';

mysql> SHOW GRANTS FOR 'username'@'localhost';

mysql> DROP USER 'username'@'localhost';


## A Basic MySQL Tutorial - 

[root@192 ~]# mysql -u root -p

### How to Create and Delete a MySQL Database

mysql> SHOW DATABASES;


mysql>  CREATE DATABASE database_name;

mysql> SHOW DATABASES;


mysql> DROP DATABASE database_name;

mysql> SHOW DATABASES;


### How to Access a MySQL Database


mysql> CREATE DATABASE events;

mysql> use events;

mysql> show tables;


### Create a MySQL Table

```
CREATE TABLE potluck (id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
name VARCHAR(20),
food VARCHAR(30),
confirmed CHAR(1), 
signup_date DATE);
```

mysql> show tables;

mysql> DESCRIBE potluck;

mysql> select * from potluck;


### How to Add Information to a MySQL Table

mysql> INSERT INTO `potluck` (`id`,`name`,`food`,`confirmed`,`signup_date`) VALUES (NULL, "John", "Casserole","Y", '2012-04-11');

mysql> select * from potluck;



### Update Information in the Table

```
UPDATE `potluck` 
SET 
`confirmed` = 'Y' 
WHERE `potluck`.`name` ='Sandy';
```

mysql> select * from potluck;


### How to Add and Delete a Column

mysql>  ALTER TABLE potluck ADD email VARCHAR(40);

mysql> select * from potluck;


mysql>  ALTER TABLE potluck ADD address VARCHAR(40) AFTER name;

mysql> select * from potluck;


mysql> ALTER TABLE potluck DROP email;

mysql> select * from potluck;


### How to Delete a Row

mysql> DELETE from potluck  where name='Sandy';

mysql> select * from potluck;

.
  
**@ By — Anup Kumar Mondal**
