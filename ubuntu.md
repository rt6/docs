# UBUNTU 16.04 LTS (XENIAL XERUS)

### Package Management (apt)
Ubuntu 16.04 introduced apt to replace apt-get.  It now has a download progress bar :smile:
You can also install and use Aptitude

```sh
# Get new packages
$ sudo apt update

# List packages that need to be updated
$ sudo apt list --upgradeable

# Download and install new packages
$ sudo apt upgrade

# show apt command line options
$ apt help

# show files/dependencies for packageName
$ apt show <packagename>
```

### SCP (Secure Copy)
```sh
# copy file to remote server using ssh config alias
$ scp <LocalFileName> <RemoteAlias>:<RemotePath>

# example
$ scp hello.txt myServer:~/path-to-dir
```
