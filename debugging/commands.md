# Userful commands

* get RAID config  `cat /proc/mdstat` →  
  
Wipe newly added disk, if it is not coming up unused under storage disk

```
fdisk -l  
wipefs /dev/<disk> -a  
lscpu: list CPU and processor info  
hwinfo: generic hardware information  
lspci: PCI busses, including graphics card, network adapter  
lsblk: list block devices (storage and partitions)  
df -h: disk free  
free -h: total, free, used RAM
```

* When there is issue that “Disk shortage (/etc/pihole/pihole-FTL.db) ahead: **94% used”**

```

sudo service pihole-FTL stop  
sudo rm /etc/pihole/pihole-FTL.db  
sudo service pihole-FTL start  
```

* https://www.reddit.com/r/pihole/comments/rpegsv/disk_shortage_error/