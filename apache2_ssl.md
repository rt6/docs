#Setup SSL on Apache2 using Self-Signed Key

```sh
# generate private key and certificate
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt

# create Diffie-Hellman group
$ sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```
