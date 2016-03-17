#### Rsync
```
rsync -avPr -e "ssh -p 10009" folder user@SERVER:/DEST/
```

#### Server stuff
* **kvm** list machines: `virsh list --all`
* **kvm** shutdown: `virsh shutdown vm-name`
* **kvm** shutdown: `connect to the machine via ssh and type "init 0"`

* **lxc** list: `lxc-ls -f`
* **lxc** shutdown: `lxc-stop --name [container-name]`



#### R Stuff
https://www.datacamp.com/community/tutorials/15-easy-solutions-data-frame-problems-r
