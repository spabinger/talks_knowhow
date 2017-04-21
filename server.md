## Server Things

### List all network cards
lspci | egrep -i --color 'network|ethernet'

### Show all ip addresses
ip addr show

### Show/manipulate network interfaces
cat /etc/network/interfaces

### IPTABLES
iptables -S
iptables -L


## Get names of interfaces
ip link


zfs list

lshw -class network

netstat -tulpen


### Find active internet connections
netstat -tulpen



## Switch

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
