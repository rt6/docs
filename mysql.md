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
grant all priviledges on <db_name>.<table> to 'user'@'localhost';
flush priviledges;

-- check users list
select * from mysql.user
```
