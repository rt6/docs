# MEDIAWIKI

### 1. Configure mediawiki to work from domain.com/wiki subdirectory URL
Install mediawiki in **/var/www/w** directory and then open from **www.domain.com/wiki**

Also rewrites (ie. removes) index.php from the URL

**LocalSettings.php**
```php
# the mediawiki script directory eg. /var/www/w
$wgScriptPath = "/w";

# the subdirectory alias "wiki"
$wgArticlePath = "/wiki/$1";

# your server IP or domain name
$wgServer = "http://XX.XX.XX.XX";
```

**apache2-site.conf**
```
<VirtualHost *:80>
  <directory /var/www/w/>
    Options Indexes FollowSymLinks MultiViews
    AllowOverride All
    Order allow,deny
    allow from all
  </Directory>
  
  ServerAdmin webmaster@localhost
  Alias /wiki /var/www/w/index.php
  RewriteEngine on
  
  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
