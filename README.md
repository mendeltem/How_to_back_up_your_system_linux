# How_to_back_up_your_system_linux

## get the dive info
```bash
lsblk

sudo mount /dev/sdb1 /media/external
```

##empty trash
```bash
rm -rf /home/*/.local/share/Trash/files/*
```

# show the folder size with exclude and max depth
`sudo du  --max-depth 1 --exclude="CSB*" /home/ | sort -h`

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

![Image 15](https://static1.makeuseofimages.com/wordpress/wp-content/uploads/2022/08/lshw-class-network-and-network-information-output.jpg?q=50&fit=crop&w=1500&dpr=1.5)


You can use the file /etc/udev/rules.d/70-persistent-net.rules to configure the logical names for the interface. To control which interface gets which logical name, you will need the physical MAC addresses of the interfaces.

You can find the line that matches the physical MAC address and change NAME=ethA to whatever you want. Reboot your system immediately afterward to save the changes.




# Configuring Ethernet Interface on Ubuntu 18.04 and Earlier


With the ethtool program, you can view settings such as auto-negotiation, duplex mode, and port speed. If ethtool is not installed on your server, you can install it using the following command:

```bash
sudo apt install ethtool

```

After the installation is complete, you can see the sample output for eth0:

```bash
sudo ethtool eth0

```

![Image 15](https://static1.makeuseofimages.com/wordpress/wp-content/uploads/2022/08/ethtool-usage-for-eth0-output.jpg?q=50&fit=crop&w=1500&dpr=1.5)

You should remember that the changes you make with the ethtool command are temporary. If you want to keep those settings, you must add the desired ethtool command to a boot statement in the /etc/network/interfaces file.

For example, you want the interface named eth0 to have a connection speed of 500MB/s running in duplex mode. To configure this permanently, you can edit the /etc/network/interfaces file as follows:


![Image 15](https://static1.makeuseofimages.com/wordpress/wp-content/uploads/2022/08/eth0-500-mbs-configuration-interfaces-file.jpg?q=50&fit=crop&w=1500&dpr=1.5)

The configuration you've seen above also works with other methods like DHCP, even if it's a static method interface.


# Configure Ethernet Interface on Ubuntu 20.04 and Later

The path you need to follow for ethernet network configuration in Ubuntu 20.04 is slightly different from older Ubuntu versions. Newer Ubuntu releases (after 18.04) now have /etc/netplan/ instead of /etc/network/interfaces.

With this folder, it is possible to make changes to the ethernet network interface. It is also straightforward to use since it contains a YAML file.

1 . Using Netplan, you can configure the static IP as follows:

```bash
ls /etc/netplan

# Output
00-installer-config.yaml

```
2. Create a backup of this file with the following command:

```bash
sudo cp /etc/netplan/00-installer-config.yaml 00-installer-config.yaml.copy

```

3. Then, open the file with your favorite text editor:


```bash
sudo vim /etc/netplan/00-installer-config.yaml
```
4. Since this is a YAML file, it's easy to make the necessary edits. Edit the file the way you want. Here is an example:

![Image 15](https://static1.makeuseofimages.com/wordpress/wp-content/uploads/2022/10/netplan-network-config-file-for-ubuntu.jpg?q=50&fit=crop&w=1500&dpr=1.5)

Hostname:
s-csb-gpu.charite.de

MAX-Adresse:
e4-1f-13-ef-ed-30

IP-Adresse:
10.47.120.23

5. After configuring your file as above, save and exit. Apply the necessary changes with the following command:

```bash

sudo netplan apply

```

6. You can now check the changes using the following command:

```bash
ip addr
```



![Image 15](https://static1.makeuseofimages.com/wordpress/wp-content/uploads/2022/10/changes-check-for-netplan-configuration-for-ubuntu-server.jpg?q=50&fit=crop&w=1500&dpr=1.5)

