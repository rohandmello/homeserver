# Home Server - Services and Configuration

## OS: Ubuntu Server 20.04 LTS

* Processor: Intel(R) Core(TM) i3-6100 CPU @ 3.70GHz, 4 cores  
* Memory: 4GB/3.79GiB(actual)  
* Disks → command to get disk info `sudo fdisk -l`  
  * `/dev/sdb : WDC WD5000LPVX-6 : 465.78 GiB`
  * `/dev/sda : WDC WD10EZEX-75W : 931.28 GiB`
  * `/dev/sdc : SanDisk SD7SB2Q- : 476.96 GiB`
  * `/dev/sdd : HGST HTS721075A9 : 698.65 GiB`
* Disk Usage  
  * `/dev/sdc` : SanDisk SD7SB2Q- : OS installed  
  
## RAID

* Create RAID during installation of the OS or after using Webmin
* Create a file system on the RAID drive
  * `/dev/mdX` → `X` = your drive number it could be any number  
* After file system is created mount the drive in one of the locations on the OS drive so that it is accessible by all the applications  
* Links to understand RAID  
  * [How to perform Software RAID](https://tldp.org/HOWTO/Software-RAID-HOWTO.html)  
  * [Recovering MD Array in mdadm](https://ahelpme.com/linux/recovering-md-array-and-mdadm-cannot-get-array-info-for-dev-md0/)  
* Remove a disk from a RAID config  
  * [Change Disk in Raid System](https://askubuntu.com/questions/992272/change-disk-in-raid-5-system)  
  
### Configuration

* RAID 5 : `/dev/md127` → `cat /proc/mdstat` → get RAID config  
  * `/dev/sdb`
  * `/dev/sda`
  * `/dev/sdd`

## Webmin

* [https://192.168.1.198:10000/](https://192.168.1.198:10000/) → server login

## Samba Share

* [https://help.ubuntu.com/community/Samba](https://help.ubuntu.com/community/Samba)  
* [https://ubuntu.com/tutorials/install-and-configure-samba\#4-setting-up-user-accounts-and-connecting-to-share](https://ubuntu.com/tutorials/install-and-configure-samba#4-setting-up-user-accounts-and-connecting-to-share)  
* **sharedfolder → usercreatedtoaccessthis:<yourpassword>**


## Jellyfin

* [http://192.168.1.198:8096/](http://192.168.1.198:8096/)  
* User: linuxusername:<yourpassword> → server login
* Currently uninstalled

## Nextcloud

* admin
  * `adminuser:<Your@password>`
* users
  * `websiteuser:<Password>`
* Server URL - local network
  * [https://192.168.1.220/index.php/login](https://192.168.1.198/index.php/login)  
* Server URL - Internet
  * [https://damelcloud.myddns.me/](https://damelcloud.myddns.me/)  
  * To Open it to internet, login to router and use port forwarding. Use HTTP then change the HTTP port to 443\. IP for forwarding is .4

### Upgrade Steps

1. Check which php is required  
2. Update all the php modules to that version [PHP Module Version](https://docs.nextcloud.com/server/latest/admin_manual/installation/php_configuration.html)  
   1. `apt install php8.5-common php8.5-curl php8.5-dom php8.5-gd php8.5-JSON php8.5-xml php8.5-mbstring php8.5-posix php8.5-zip php8.5-mysql php8.5-intl php8.5-ftp php8.5-smbclient php8.5-bcmath php8.5-gmp php8.5-memcached php8.5-apcu php8.5-redis`
3. Follow these steps  
   1. `sudo -u www-data php occ maintenance:mode --on`
   2. `apt-get reinstall libapache2-mod-php8.5`
   3. `a2enmod php8.5`
   4. `a2dismod php8.3`
   5. `systemctl restart apache2`
   6. `for linkgroup in $(ls /var/lib/dpkg/alternatives/ | grep -E "ph(ar|p)"); do sudo update-alternatives --config $linkgroup; done`
   7. `sudo -u www-data php occ maintenance:mode --off`
4. Update this values in `php.ini` at `/etc/php/8.5/apach2/php.ini`
   1. `max_execution_time = 500` (to keep the web updater from timing out)
   1. `max_input_time = 600` (to keep the web updater from timing out)
   1. `memory_limit = 2G` (required)
   1. `post_max_size = 5G` (this is required because of below setting)
   1. `upload_max_filesize = 5G` (for large uploads)  
5. Remove Older version of PHP only after you are confident that update is completed successfully
   1. `sudo apt purge "php8.3*"`
## **Mysql**

* root:<Your@password>  
* databaseuser:<Your@password>  
* DBname: nextclouddb

## **ngrok**

* Authtoken saved in /root/.config/ngrok/ngrok.yml  
* Ngrok run in background → `nohup ngrok start --all --log=stdout > ngrok.log &`
* Ngrok config file →

```

authtoken: 1qx4KqQhBrKUQEktAEPHWFwpI7f_nWjTx9ULN1TueKBohnPq
version: 2  
tunnels:  
  tunnel_to_next:  
    proto: http  
    hostname: trusting-stingray-related.ngrok-free.app  
    addr: <https://192.168.1.198>

    \# \-------------------------  
    \# Additional options  
    \# \-------------------------  
    \# auth: "username:password"  
    \# host\_header: rewrite  
    \# inspect: true  
    \# bind\_tls: true
```

## Vaultwarden

* [Install Vault warden without docker](https://www.bloovis.com/posts/2023-10-06-vaultwarden-without-docker/)

```
/opt/vaultwarden/vaultwarden hash
Password : <Your@password>  
ADMIN_TOKEN=<token>

```
