# Virtual Box

## Resize Virtual Machines (MacOS Host and Ubuntu Guest)

**Important:** Switch off VM before proceeding.


1) On the `MacOS Host`: 
```sh
# go to Virtual Box directory
cd /Applications/VirtualBox.app/Contents/MacOS/

# resize vdi file.  The new size is in megabytes so 20000 = 20 GB
VBoxManage modifyhd --resize 20000 /Users/rtdev/VirtualBox\ VMs/my-vm/my-vm.vdi

# check that the vdi has been resized
VBoxManage showhdinfo /Users/rtdev/VirtualBox\ VMs/my-vm/my-vm.vdi
```




2) Now on the `Ubuntu Guest`: 

Turn on VM and use `gparted` on Ubuntu to modify partitions to use the additional harddisk space. 

```sh
# install gparted (partition manager with GUI)
sudo apt-get install gparted

# run gparted
# You may need to delete turn off swapoff and then delete the extended partition containing the swap.  
# Then resize primary partition /dev/sda1 and re-create the linux-swap parition.
sudo gparted

# Now reboot and check for additional hard disk space and new swap partition
df -h
```



