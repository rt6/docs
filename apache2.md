# APACHE2 for Ubuntu 16.04

### Basic
````sh
$ sudo service apache2 start
$ sudo service apache2 stop
$ sudo service apache2 restart
$ sudo service apache2 reload
````

### Virtual Hosts (Setup multiple web apps/domain names on one server)
Create a `.conf` file for each web app/domain name in the `/etc/apache2/sites-available/` directory and ensure `ServerName` and `DocumentRoot` fields have a value.
````xml
<VirtualHost *:80>
  ServerAdmin webmaster@subdomain.tld.com
  DocumentRoot "/www/docs/subdomain.tld.com"
  ServerName subdomain.tld.com
  ErrorLog "logs/subdomain.tld.com-error_log"
  TransferLog "logs/subdomain.tld.com-access_log"
</VirtualHost>
````

### Enable ReWrite
```sh
$ sudo a2enmod rewrite
$ sudo systemctl restart apache2
```


### Add and remove virtual hosts
```sh
# add virtual host to sites-enabled directory
$ sudo a2ensite <conf file>

# remove virtual host from sites-enabled directory
$ sudo a2dissite <conf file>

# remember to restart apache each time there are changes to virtual hosts
$ sudo service apache restart
```


### Multiple web apps using the SAME domain name (aka mapping domain name paths and the file system)
In this example, the `domain.com` (the root /) path will use files in `/var/www/app1` and `domain.com/app2` path will use files in `/var/www/app2`:

```
<VirtualHost *:80>
  DocumentRoot /var/www/app1
  Alias "/app2" "/var/www/app2"
</VirtualHost>
```

