### Mount MS Windows Share

#### Install packages
sudo apt-get install smbfs

#### Mount device
sudo mount -t cifs //SERVER/SHARE /mnt/DEST/ -o user=USER,domain=DOMAIN,uid=1000,gid=1000,dir_mode=0777,file_mode=0777


### Mount USB
#### Find out the device location
> lsblk
#### Mount
> mkdir usb_ait
> mount -t ntfs /dev/sdm1 usb_ait

### KVM mount USB
Connect with x2go to the host machine
go to virtual machine manager --> open the vm --> add hardware -> USB Host Device, select the right usb, and restart the vm 
