# Userful commands

###  Get RAID config  
1. `cat /proc/mdstat` →  
  

### Wipe newly added disk, if it is not coming up unused under storage disk

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

### When there is issue that “Disk shortage (/etc/pihole/pihole-FTL.db) ahead: **94% used”**

```

sudo service pihole-FTL stop  
sudo rm /etc/pihole/pihole-FTL.db  
sudo service pihole-FTL start  
```

* https://www.reddit.com/r/pihole/comments/rpegsv/disk_shortage_error/


### Create new directory for sambashare to be accessed over the network 

1. Login with the user who can access the `root` privileges with `sudo`
1. create a directory with name you want to `sudo mkdir dirname`
1. create a user if you want to add the new user for this dir's access `sudo useradd username`
1. set the password for the newly created user `sudo passwd username` 
1. if the user is going to be used on samaba share you need to set its password seperately `sudo smbpasswd -a username`
1. create a group if you want the user to be member of group `sudo groupadd groupname`
1. add user to the gorup `sudo usermod -aG username groupname`
1. update directory premissions `sudo chown -R username:gorupname /home/localuser`