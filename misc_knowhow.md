### Rsync
```
rsync -avPr -e "ssh -p 10009" folder user@SERVER:/DEST/
```

### Server stuff
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
**lxc** start: `lxc-start --name [container-name] -d`
**lxc** reboot: `lxc-stop  --name [container-name] -r`



### R Stuff
https://www.datacamp.com/community/tutorials/15-easy-solutions-data-frame-problems-r
