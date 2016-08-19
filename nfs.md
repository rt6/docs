# NFS

```sh

# install nfs client
$ sudo apt install nfs-common

# mount remove nfs directory
$ sudo mount <nfs server ip and directory> <local directory>
$ sudo mount 1.1.1.1:/data01 /mnt/dir1

# check disk space
$ df -h

# check nfs version
$ nfsstate -m 


```
