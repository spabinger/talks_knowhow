## Install packages
sudo apt-get install smbfs

## Mount device
sudo mount -t cifs //<SERVER>/<SHARE> /mnt/<DEST>/ -o user=<USER>,domain=<DOMAIN>
