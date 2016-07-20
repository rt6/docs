# OpenStack

### Create and Mount Volume Storage
1. Create volume storage in dashboard and mount to instance

2. SSH to VM instance
```sh
# list block devices that you can mount
# note: vda is the root disk of the system with one partition called vda1
# the block storage might be called vdb, vdc, etc...
$ sudo fdisk -l
$ lsblk

# format block
$ sudo mkfs.ext4 /dev/vdc

# create mount path directory
$ sudo mkdir /mnt/volume_storage

# mount block to path
$ sudo mount /dev/vdc /mnt/volume_storage/

# check disk free 
$ df -lh
```
