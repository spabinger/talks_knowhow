### :: TOC ::
[Docker](#docker) <br/>
[IPMI](#ipmi) <br/>
[IPTABLES](#iptables) <br/>
[LXC](#lxc) <br/>
[ZFS](#zfs) <br/>




### :: Update Server ::
https://help.ubuntu.com/lts/serverguide/installing-upgrading.html
``` do-release-upgrade ```


### :: Network ::

* List all network cards <br/>
``` lspci | egrep -i --color 'network|ethernet' ```

* Show all ip addresses <br/>
``` ip addr show ```

* Show/manipulate network interfaces <br/>
``` cat /etc/network/interfaces ```

* Check speed / connection of network cards <br/>
``` ethtool <eth0> ```

* Get names of interfaces <br/>
``` ip link ```

* Port forwarding <br />
``` /etc/rc.local ```

* Virtual networks <br />
https://en.wikipedia.org/wiki/Virtual_network <br />
https://linuxconfig.org/configuring-virtual-network-interfaces-in-linux <br />

* Reload an interface (e.g., after changing /etc/network/interfaces) <br />
``` sudo ifdown <interface> && sudo ifup <interface> ``` <br />
``` sudo service networking restart ```

<a name="iptables" /> <br/>
#### IPTABLES
* List IPTABLES <br/>
``` iptables -S ``` <br />
``` iptables -L ```

* IPTABLES Links <br/>
https://help.ubuntu.com/community/IptablesHowTo

* Portforwardings settings <br/>
``` Rules are set in /etc/rc.local ```

* Portforwarding: show current setup <br/>
```iptables -t nat -v -L -n --line-number```

* Portforwarding: set rule <br/>
```iptables -t nat -A PREROUTING -i br0 -p tcp -m tcp --dport PORT -m comment --comment "COMMENT" -j DNAT --to-destination xxx.xxx.xxx.xxx:PORT``` <br />
Example: <br />
```iptables -t nat -A PREROUTING -i br0 -p tcp -m tcp --dport 10002 -m comment --comment "My-LXC" -j DNAT --to-destination 10.0.0.10:22``` <br />

* Portforwarding: Delete rule (use line number) <br/>
https://www.cyberciti.biz/faq/how-to-iptables-delete-postrouting-rule/ <br />
``` iptables -t nat -D PREROUTING 3 ```




#### XXX
``` lshw -class network ```


* Find active internet connections <br/>
``` netstat -tulpen ```


### :: Disks ::

* Display block devices <br/>
``` blkid -o list ```

* Display all disks <br/>
``` 
parted
print all
```



<a name="zfs" /> <br/>
### :: ZFS ::

* List all zfs-folders/zfs-volumes <br/>
``` zfs list ```

* Status of zpool <br/>
``` zpool status ```

* Export zpool (unmount)<br/>
``` zpool export <zpoolname> ```

* Remove/destroy <br/>
``` zpool destroy <zpoolname> ```

* ZFS Raid levels <br/>
http://www.zfsbuild.com/2010/05/26/zfs-raid-levels/

* Improve performance of ZFS <br/>
https://icesquare.com/wordpress/how-to-improve-zfs-performance/

* ZFS RAID level performance <br/>
https://icesquare.com/wordpress/zfs-performance-mirror-vs-raidz-vs-raidz2-vs-raidz3-vs-striped/
https://calomel.org/zfs_raid_speed_capacity.html

* ZFS Cache <br/>
http://serverascode.com/2014/07/03/add-ssd-cache-zfs.html

* More information on ZFS <br/>
http://breden.org.uk/2009/05/10/home-fileserver-zfs-file-systems/


<a name="docker" /> <br/>
### :: Docker ::

* Cheat-sheet <br/>
https://github.com/wsargent/docker-cheat-sheet

* List Running containers <br/>
``` docker ps -a ```

 * Create image from Dockerfile <br/>
 ``` docker build ```

* Create and start a container in one operation <br/>
``` docker run 
-d         detach
--name     Name of the container
--restart  Automatically restart the container -  no, always
-p         Ports
-v         Bind a volume
```

* Look at all the info on a container (including IP address) <br/>
``` docker inspect ```

* Delete a container <br/>
``` docker rm ```



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



<a name="kvm" /> <br/>
### :: KVM ::

**kvm** list machines: `virsh list --all` <br />
**kvm** shutdown: `virsh shutdown vm-name` <br />
**kvm** shutdown: `connect to the machine via ssh and type "init 0"` <br />
**kvm** start:  `virsh start vm-name`

<a name="lxc" /> <br/>
### :: LXC ::

* LXC information: <br />
http://www.cyberciti.biz/faq/howto-forcefully-stop-and-kill-lxc-container-on-linux/ <br />
https://help.ubuntu.com/lts/serverguide/lxc.html <br />

* List machines: <br/>
`lxc-ls -f`
* Shutdown: <br/>
`lxc-stop --name [container-name] --nokill` <br />
* Start: <br/>
`lxc-start --name [container-name] -d` <br />
* Reboot: <br/>
`lxc-stop --name [container-name] -r` <br />
* Attach: 
`lxc-attach -n [container-name] ` <br />
run command inside container
* Copy from one host to another <br />
Simply copy the folder in /var/lib/lxc
* LXC on ZFS: <br />
https://www.scotte.org/2016/07/lxc-containers-on-zfs
* Networking <br />
http://containerops.org/2013/11/19/lxc-networking/


### :: Services ::
* List all running services <br />
``` service --status-all ```



SSH
https://help.ubuntu.com/lts/serverguide/openssh-server.html






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



