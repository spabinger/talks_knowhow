#### Rsync
```
rsync -avPr -e "ssh -p 10009" folder user@SERVER:/DEST/
```

#### Server stuff
**kvm** list machines: `virsh list --all` <br />
**kvm** shutdown: `virsh shutdown vm-name` <br />
**kvm** shutdown: `connect to the machine via ssh and type "init 0"` <br />

**lxc** list: `lxc-ls -f` <br />
**lxc** shutdown: `lxc-stop --name [container-name]` <br />



#### R Stuff
https://www.datacamp.com/community/tutorials/15-easy-solutions-data-frame-problems-r
