# SaltStack

## 1. Setup Masterless Minion
---

###Boostrap minion

```sh
$ curl -L https://bootstrap.saltstack.com -o bootstrap_salt.sh
$ sudo sh bootstrap_salt.sh

# create basic minion config file at path /etc/salt/minion.d/example.conf (see example below)

# stop salt-minion because it does not need to talk to master
$ sudo service salt-minion stop

# make directory to store minion configs
$ mkdir -p /srv/salt/base

# create top.sls file to store minion configs (see example below)
$ vi /srv/salt/base/top.sls
```

### Basic minion config file 
Store at path `/etc/salt/minion.d/example.conf`
This will overwrite /etc/salt/minion
```yaml
file_client: local
file_roots:
  base:
    - /srv/salt/base
  ci:
    - /srv/salt/ci
  base_optional:
    - /srv/salt/anotherbase
```

### Basic top.sls file 
Store at path `/srv/salt/base/top.sls`

Each directory will have a top.sls file that contains the necessary state configurations
```yaml
base:
    '*':
        - update_ubuntu
        - vim
        - ssh
        - lamp_server
        - git
```

### Update minion with states
```sh
$ sudo salt-call --local state.highstate -l debug
```

# 2. Setup Salt-master and Salt-minion
---

### Boostrap salt master using latest version from github
Note this 2-step process allows you to inspect the sh script to ensure it is what is is !
```sh
$ curl -o install_salt.sh -L https://bootstrap.saltstack.com
$ sudo sh install_salt.sh -P -M -N git v2016.3.0rc2
```

## Bootstrap salt minion
```sh
$ curl -o install_salt.sh -L https://bootstrap.saltstack.com
$ sudo sh install_salt.sh -P git v2016.3.0rc2
```

### help with bootstrap script
```sh
$ sh bootstrap-salt.sh -h
```

### Add the IP or DNS name of the master to the minion
Ensure [4505 and 4506](https://docs.saltstack.com/en/latest/topics/tutorials/firewall.html) is open on the master, and then on the minon, `/etc/salt`:
```
master: <salt master ip or dns_name>
```

Now run this command to try to connnect to salt-master  (it won't work because the master has not accepted the key of the minion)
```
$ sudo salt-mionion -l debug
```

on the salt-master
```
# list fingerprints of all keys (including the master's own key, and incoming minion requests)
$ salt-key -F master
```

copy the master.pub fingerprint and add to minion /etc/salt/minion file
```
master_finger: '<master.pub value>'
```

on the master request for the minion's fingerprint. note: <minion-d> can be found in /etc/salt/minion_id
```
$  salt-key -f <minion-id>
```

on the minion, check its own key fingerprint
```
$ salt-call key.finger --local
```

if they both match , then you can accept the minions key and this will connect the master with the minion
```
# accept minion's key
$ salt-key -a <minion-id>

# now the minion will be in the accepted list (green)
$ sudo salt-key -L
```

test connection on salt-master
```
$ sudo salt '*' test.ping
```
