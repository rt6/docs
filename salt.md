# SaltStack

## 1. Masterless Minion

###Boostrap minion

```sh
$ curl -L https://bootstrap.saltstack.com -o bootstrap_salt.sh
$ sudo sh bootstrap_salt.sh

# stop salt-minion because it does not need to talk to master
$ sudo service salt-minion stop
```
