#MYSQL

### Start and stop MySQL
```sh
$ sudo /etc/init.d mysql start
$ sudo /etc/init.d mysql status
$ sudo /etc/init.d mysql stop
```

### Login from command line
```sql
$ mysql -u<username> -h <dhostname>:<port> -p<password> 
```

### Check user priviledges
```sql
show grants;
show grants for 'user'@'localhost';
```

### Create and grant new user
```sql
create user 'user'@'localhost';
grant all privileges on <db_name>.<table> to 'user'@'localhost';

# for example
grant all privileges on *.* to 'new_admin_user'@'localhost';

flush privileges;

-- check users list
select * from mysql.user
```

### Backup Database or Migrate Database to another Machine
```sh
# export databases (on source machine)
$ mysqldump --quick [database_name] > [database_name].sql
$ mysqldump --quick [database_name] -h [host] -u[username] -p[password] > [database_name].sql
```

```sql
# create new databse (on target machine)
> mysql
> create database [new database name];
> exit;
```

```sh
# import database (on the target machine)
$ mysql -h [host] -u[username] -p [new database name] < [database_name].sql

```


### Check mysql configs
```sh
# mysql daemon path
$ which mysqld

# print order that default options (mysql configs) files are read
$ /usr/sbin/mysqld --verbose --help | grep -A 1 "Default options"

> Default options are read from the following files in the given order:
> /etc/my.cnf /etc/mysql/my.cnf ~/.my.cnf

#or try
$ mysqld --print-defaults

````


## Import and Export databses for migration
Use MySQL `mysqldump` command line tool
```sh
# to export
$ mysqldump -u mysql_user -p DATABASE_NAME > backup.sql
 
# to import 
$ mysql -u mysql_user -p DATABASE < backup.sql
```


### SSH Tunnel to access MYSQL 
Access a remote MySQL using a local GUI/CLI (eg. MySQL Workbench)
```sh
# syntax 
ssh -L 3306:<bind-address>:3306 username@server-ip -i private-key -N

# examples
ssh -L 3306:127.0.0.1:3306 ubuntu@1.2.3.4 -i mykey -N

# or if you have setup ssh config file for this host (mysqlserver1)
ssh -L 3306:127.0.0.1:3306 mysqlserver1 -N
```
