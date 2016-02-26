## Install packages
sudo apt-get install smbfs

## Mount device
sudo mount -t cifs //SERVER/SHARE /mnt/DEST/ -o user=USER,domain=DOMAIN,uid=1000,gid=1000,dir_mode=0777,file_mode=0777
