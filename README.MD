Allows easy use to control the ClusterHAT made by 8086, split into 2 parts.
1. ClusterHAT control (Currently this only supports the ClusterHAT v2.2, as this is the only one I own.)
2. USBBoot Utils

## ClusterHAT control
Provides a simple interface for the i2c commands used by the ClusterHAT (v2.2) 
### init
Initialises the ClusterHAT to allow I2C commands
### on | off [element]
```i2cset -y -m MASK 1 0x20 1 ON|OFF```
```i2cset -y -m $((2#MASK)) 1 0x20 1 ON|OFF```
| | MASK | ON | OFF |
|---|---|---|---|
| USB 1 | 1 | 0xff | 0x00 |
| USB 2 | 2 | 0xff | 0x00 |
| USB 3 | 4 | 0xff | 0x00 |
| USB 4 | 8 | 0xff | 0x00 |
| Status LED's | 16 | 0xff | 0x00 |
| USB Hub ** | 32 | 0x00 | 0xff |
| Alert LED | 64 |0xff | 0x00 |
| Write Protection | 128 | ? | ? |

**NOTE: for this version (v2.2) the HUB's on & off commands are inversed from the rest of the other elements



## USBBoot Utils

### bind ( and unbind ) [ enable / disable ]
Binds a usb path named folder to a boot folder
Specify both USB Path and either a full path or a name (which the full path can be calculated from the config) 
`bind 1-1.3.2 /var/lib/clusterhat/nodes/orange/boot` or the simpler `bind 1-1.3.2 orange`
[unbind does the opposite, and unbinds anything bound with this command]

### boot
Manually calls for the boot (alias for rpiboot). 
Optionally specify the boot directory to boot from, or leave blank to use the config defined location

### clean
Resets the specified node by deleting the VFS/OFS and resetting it back to the base OS

### create
Creates a node by specifying either name or a full path. By specifying just a name, the full path will be calculated from the config. 



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


## Modules
### Enable IPv4 routing
net.ipv4.ip_forward=1
