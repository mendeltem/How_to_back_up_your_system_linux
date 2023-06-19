# How_to_back_up_your_system_linux
```bash
sudo rsync -aAXv --dry-run --delete --exclude=/dev/* --exclude=/proc/* --exclude=/sys/* --exclude=/tmp/* --exclude=/run/* --exclude=/mnt/* --exclude=/media/* --exclude="swapfile" --exclude="lost+found" --exclude=".cache" --exclude="Downloads" --exclude=".VirtualBoxVMs" --exclude=".ecryptfs" --exclude="CSB_NeuroRad*" --exclude="PROSCIS" --exclude="PRO" /* /home/temuuleu/CSB_NeuroRad/Z_Allgemein/Server_backups/gpu_server/
```
