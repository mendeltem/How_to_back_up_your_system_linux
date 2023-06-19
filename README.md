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

```bash
ifconfig -a | grep eth

# Output
eth0: flags=4098 mtu 1500
```

