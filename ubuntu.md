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

### Rsync (Copy files to another mounted storage)
``` sh
# dry run to see what files will be copied across
# note: the "/" in source-dir is importan.  It means you want to copy contents in source-dir to target-dir
# if you omit the "/" then source-dir will be copied to target-dir/source-dir/
$ rsync -anv source-dir/ target-dir

# if you are happy with the dry-run then proceed with rsync
# the -a means "archive and will copy all symlinks, files, and directories
$ rsync -a source-dir/ target-dir

```


### SSH 
Add a public key to remove server in one command 
```sh
$ cat ~/.ssh/id_rsa.pub | ssh user@hostname 'cat >> .ssh/authorized_keys'
```
