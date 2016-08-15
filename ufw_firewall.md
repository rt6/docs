#UFW Firewall
Command line front-end for ip tables.

```sh
$ sudo apt install ufw

$ sudo ufw status verbose

# port number
$ sudo ufw allow 22

$ sudo ufw default deny incoming

$ sudo ufw default allow outgoing  

# common service names: ssh, http, https
$ sudo ufw allow ssh 

# port range
$ sudo ufw allow 10000:10001/tcp
$ sudo ufw allow 10000:10001/udp

# public network or private network
$ sudo ufw allow in on eth0 to any port 80
$ sudo ufw allow in on eth1 to any port 3306

# make sure you enable port 22 before enabling ufw, otherwise you will be locked out !
$ sudo ufw enable 
```
