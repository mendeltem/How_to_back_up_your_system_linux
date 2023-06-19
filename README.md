# How_to_back_up_your_system_linux

## create a backup

```bash
sudo rsync -aAXv --dry-run --delete --exclude=/dev/* --exclude=/proc/* --exclude=/sys/* --exclude=/tmp/* --exclude=/run/* --exclude=/mnt/* --exclude=/media/* --exclude="swapfile" --exclude="lost+found" --exclude=".cache" --exclude="Downloads" --exclude=".VirtualBoxVMs" --exclude=".ecryptfs" --exclude="CSB_NeuroRad*" --exclude="PROSCIS" --exclude="PRO" /* gpu_server/
```

## restore your system

```bash

sudo rsync -aAXv --delete --exclude="lost+found" gpu_server/user/bin/ /usr/bin/
sudo rsync -aAXv --delete --exclude="lost+found" gpu_server/user/lib/ /usr/lib/

```


# Managing Ethernet Interfaces on Ubuntu

An Ethernet networking interface is a circuit board with an Ethernet port that enables your computer to establish an Ethernet connection. Ethernet interfaces have a simple naming convention. The first Ethernet interface is typically eth0. Then comes eth1. All additional interfaces are named like this.

To view the available Ethernet interfaces, run the following ifconfig command:

```bash
ifconfig -a | grep eth

# Output
eth0: flags=4098 mtu 1500
```

With the lshw command, you can define all the network interfaces you need for configuring networks on Ubuntu. Below you will see an example command. This command will display bus information, driver details, and all its supported capabilities as a single Ethernet interface:

```bash
sudo lshw -class network

```
![Image 15]([images/image_1.jpg](https://static1.makeuseofimages.com/wordpress/wp-content/uploads/2022/08/lshw-class-network-and-network-information-output.jpg?q=50&fit=crop&w=1500&dpr=1.5))




