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
curl -o install_salt.sh -L https://bootstrap.saltstack.com
sudo sh install_salt.sh -P -M -N git v2016.3.0rc2
```

## Bootstrap salt minion
```sh
curl -o install_salt.sh -L https://bootstrap.saltstack.com
sudo sh install_salt.sh -P git v2016.3.0rc2
```
