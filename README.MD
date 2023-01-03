Allows easy use to control the ClusterHAT made by 8086
Currently this only supports the ClusterHAT v2.2, as this is the only one I own. 


### bind ( and unbind ) [ enable / disable ]
Binds a usb path named folder to a boot folder
Either specify a boot folder manually or leave blank to calculate it from config
`bind 1-1.3.2 /var/lib/clusterhat/nodes/1/boot` or the simpler `bind 1-1.3.2`
[unbind does the opposite, and unbinds anything bound with this command]

### boot
Manually calls for the boot (alias for rpiboot). 
Optionally specify the boot directory to boot from, or leave blank to use the config defined location

### clean
Resets the specified node by deleting the VFS/OFS and resetting it back to the base OS

### init
Initialises the ClusterHAT to allow I2C commands

### mount (and unmount )
Mounts all the neccesary folders for the NFS to run properly. 
Either specify a node name (then the path will be calculated using the config), a full path to the node's folder, or empty to just mount the root OS's for the nodes. 
Any form of this command will mount the root OS's before continuing. 
[unmount does the opposite, and unmounts anything mounted with this command] 

### setup
Sets up the specified node fully
1. mounts root OS's
2. mounts the node
3. setup the neccessary files
4. bind node boot directory 

