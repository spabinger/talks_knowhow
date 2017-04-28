### :: TOC ::
[ZFS](#zfs) <br/>
[IPMI](#ipmi)


### :: Network ::

* List all network cards <br/>
``` lspci | egrep -i --color 'network|ethernet' ```

* Show all ip addresses <br/>
``` ip addr show ```

* Show/manipulate network interfaces <br/>
``` cat /etc/network/interfaces ```

* IPTABLES <br/>
``` 
iptables -S
iptables -L 
```

* Get names of interfaces <br/>
``` ip link ```

#### XXX
``` lshw -class network ```


* Find active internet connections <br/>
``` netstat -tulpen ```


### :: Disks ::

#### Display block devices
``` blkid -o list ```




<a name="zfs" />

### :: ZFS ::

* List all zfs-folders/zfs-volumes <br/>
``` zfs list ```

* Status of zpool <br/>
``` zpool status ```

* ZFS Raid levels 
``` http://www.zfsbuild.com/2010/05/26/zfs-raid-levels/ ```

* Improve performance of ZFS
``` https://icesquare.com/wordpress/how-to-improve-zfs-performance/#section9 ```



### :: Docker ::

#### List Running containers
``` docker ps -a ```


<a name="ipmi" />

### :: IPMI ::
https://www.thomas-krenn.com/de/wiki/IPMI_Grundlagen
https://help.ubuntu.com/community/IPMI
https://www.thomas-krenn.com/de/wiki/IPMI_Konfiguration_f%C3%BCr_Supermicro_Systeme
https://www.thomas-krenn.com/de/wiki/Softwaretools_f%C3%BCr_IPMI_im_%C3%9Cberblick


### :: Switch ::

#### Dell 5500
"Although they can work in small EQL (and other iSCSI) SAN networks they should be seen as campus-access switches and not as SAN switches."
https://en.wikipedia.org/wiki/Dell_PowerConnect#5500_series



## Virtualization

##### KVM

**kvm** list machines: `virsh list --all` <br />
**kvm** shutdown: `virsh shutdown vm-name` <br />
**kvm** shutdown: `connect to the machine via ssh and type "init 0"` <br />
**kvm** start:  `virsh start vm-name`

##### LXC
LXC information
http://www.cyberciti.biz/faq/howto-forcefully-stop-and-kill-lxc-container-on-linux/

**lxc** list: `lxc-ls -f` <br />
**lxc** shutdown: `lxc-stop --name [container-name] --nokill` <br />
**lxc** start: `lxc-start --name [container-name] -d` <br />
**lxc** reboot: `lxc-stop  --name [container-name] -r`









Exchange a defect harddisk
Last edited by mücahit 5 months ago Page History
Exchange the defect disk
When you find out that a disk is defect, you should change it with a new one.
After you changed it you must also replace the defect disk-id with the new disk-id in the zpool:
you see the defect harddisk with the command:
zpool status
if there is a disk with the state UNAVAILABLE, that should be exchanged with a new disk
to replace the defect disk-id you need this command:
zpool replace tank [defect-disk-id] [new-disk-id]
to see that its really replaced type in again:
zpool status
if you see that the zpool is resilvering, then you are done.
NOTE: resilvering can take long time, thats normal.
Send the defect disk to the manufacturer
go to website: https://westerndigital.secure.force.com/ind/ID_Login
register the disks with their ID
create a RMA with the defect disks
click on "View RMA Premailer"
click on print, print it out and put it in and on the packet
bring the packet to the mail



