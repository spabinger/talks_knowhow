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

netstat -tulpen


### Find active internet connections
netstat -tulpen
