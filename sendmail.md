# Postfix

Best to use postfix instead of sendmail.

```
to be added ...
```




# Sendmail

Some php applications use this to send emails

# Setup
Check if sendmail is already installed
```
$ ps -e | grep "sendmail"
```
Download packages
```sh
$ sudo apt install sendmail
```
add the following line of code to these 2 files to use TLS: `/etc/mail/sendmail.mc` and `/etc/mail/submit.mc`
```
include(`/etc/mail/tls/starttls.m4')dnl
```
Configure sendmail
```
$ sudo sendmailconfig
```
Restart sendmail
```
$ sudo service sendmail restart
```

