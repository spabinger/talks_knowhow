### :: TOC ::
[Docker](#docker) <br/>
[IPMI](#ipmi) <br/>
[IPTABLES](#iptables) <br/>
[LXC](#lxc) <br/>
[Network](#network) <br/>
[Visudo](#visudo) <br/>
[ZFS](#zfs) <br/>




### :: Update Server ::
https://help.ubuntu.com/lts/serverguide/installing-upgrading.html
``` do-release-upgrade ```

<a name="network" /> <br/>
### :: Network ::

* Hints
  * Do not mix ```ifconfig XX up``` with ```ifup XXX```
  * If ```ifup``` is not working use ```--force```
  * Handle ```service networking restart``` with care
  * Do not specify 2 or more gateways on the same interface
  * Shut down interfaces: ```sudo ip link set eth0 down```
  * Remove virtual interface: ```ifconfig eth0:1 down```
  * Good ifup, ifdown description: https://www.computerhope.com/unix/ifup.htm

* Check state of interfaces
```cat /run/network/ifstate```

* List all network cards <br/>
``` lspci | egrep -i --color 'network|ethernet' ```

* Show all ip addresses <br/>
``` ip addr show ```

* Show interfaces and their name <br/>
``` lshw -class network```

* Show/manipulate network interfaces <br/>
``` cat /etc/network/interfaces ```

* Check speed / connection of network cards <br/>
``` ethtool <eth0> ```

* Network class <br/>
``` lshw -class network ```

* Find active internet connections <br/>
``` netstat -tulpen ```

* Get names of interfaces <br/>
``` ip link ```

* Services listening on port <br/>
``` lsof -nPi tcp:the-port ```

* Port forwarding <br />
``` /etc/rc.local ```

* Check speed between two servers <br/>
  * ```sudo apt-get install iperf```
  * We'll start an iperf server on one of the machines: <br/>
  ```iperf -s```
  * And then on the other computer, tell iperf to connect as a client:<br/>
  ```iperf -c <address of other computer>```

* Login problems via SSH <br/>
Getting a ```pam_systemd(sshd:session): Failed to stat runtime dir: No such file or directory``` message:
Added directory with user_id in ```/run/users/```

* Chaging DNS resolving <br/>
  * ``` sudo nano /etc/resolvconf/resolv.conf.d/base ```
  * ``` sudo resolvconf -u```

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




### :: Disks ::

* Display block devices <br/>
``` blkid -o list ```

* Display all disks <br/>
``` 
parted
print all
```

* Display all SCSI disks <br/>
```lsscsi -s```



<a name="zfs" /> <br/>
* http://docs.oracle.com/cd/E19253-01/820-2313/6ndu3p9cf/index.html
* http://docs.oracle.com/cd/E19253-01/820-2313/6ndu3p9cd/index.html
* http://docs.oracle.com/cd/E19253-01/820-2313/gbiqe/index.html
* http://docs.oracle.com/cd/E19253-01/819-5461/gbinw/

### :: ZFS ::
* List all zfs-folders/zfs-volumes <br/>
``` zfs list ```

* Status of zpool <br/>
``` zpool status ```

* Export zpool (unmount)<br/>
``` zpool export <zpoolname> ```

* Remove/destroy <br/>
``` zpool destroy <zpoolname> ```

* Show snapshots <br/>
``` zfs list -t snapshot ```

* Show iostats <br/>
``` zpool iostat 2 ```
* Show detailed io <br/>
``` sudo zpool iostat -v <pool> ```

* Send a ZFS snapshot <br/>
``` zfs send -v storage/xxx@29062017 | pv -B 1g | ssh xxx.xxx.xxx.xxx zfs receive storage/xxx ```

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

* Understanding the spaces used by ZFS <br/>
https://blogs.oracle.com/observatory/understanding-the-space-used-by-zfs

<a name="docker" /> <br/>
### :: Docker ::

* Cheat-sheet <br/>
https://github.com/wsargent/docker-cheat-sheet

* List Running containers <br/>
``` docker ps -a ```

 * Create image from Dockerfile <br/>
 ``` docker build ```

* Create and start a container in one operation <br/>
``` 
docker run 
-d         detach
--name     Name of the container
--restart  Automatically restart the container -  no, always
-p         Ports
-v         Bind a volume
```
creates and starts a container

* Docker start <br/>
starts a container

* Look at all the info on a container (including IP address) <br/>
``` docker inspect ```

* Delete a container <br/>
``` docker rm ```

* Connect to docker <br/>
```docker exec -it <containerIdOrName> bash```

* Problem loading packages during docker build <br/>
https://stackoverflow.com/questions/42064246/failed-to-establish-a-new-connection-errno-2-name-or-service-not-known
```
sudo nano /lib/systemd/system/docker.service Add the dns after ExecStar. --dns 10.252.252.252 --dns 10.253.253.253 Should look like that: ExecStart=/usr/bin/dockerd -H fd:// --dns 10.252.252.252 --dns 10.253.253.253

systemctl daemon-reload
sudo service docker restart
```

* Change port binding of existing container <br/>
https://stackoverflow.com/questions/19335444/how-do-i-assign-a-port-mapping-to-an-existing-docker-container
```
1) stop the container 
2) change the file /var/lib/docker/containers/[hash_of_the_container]/hostconfig.json
3) restart your docker engine (to flush/clear config caches)
4) start the container
```



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
* Backup <br />
https://stackoverflow.com/questions/23427129/how-do-i-backup-move-lxc-containers
```
lxc-stop -n $NAME
cd /var/lib/lxc
tar --numeric-owner -czvf container_fs.tar.gz $NAME
rsync -avh container_fs.tar.gz user@newserver:/var/lib/lxc/
rsync -avPrh -e "ssh -p 10009" folder user@SERVER:/DEST/
```


### :: Services ::
* List all running services <br />
``` service --status-all ```

<a name="visudo" /> <br/>
### :: Visudo ::
```sudo visudo```
Be aware that adding a user to the *sudo* group overrides the entries in sudoers


### :: SSH ::
https://help.ubuntu.com/lts/serverguide/openssh-server.html

### :: Resources ::
* Memory <br/>
http://www.linuxatemyram.com/

### :: RSYNC ::

* Use only limited bandwith:<br/>
``` rsync --bwlimit=<kb/second> <source> <dest> ```





