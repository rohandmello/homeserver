# Issues and resoulutions

## When there is issue that “Disk shortage (/etc/pihole/pihole-FTL.db) ahead: **94% used”**

```
1. sudo service pihole-FTL stop  
2. sudo rm /etc/pihole/pihole-FTL.db  
3. sudo service pihole-FTL start  
4. https://www.reddit.com/r/pihole/comments/rpegsv/disk\_shortage\_error/  
```

* Mount USB and copy files to it  
  * [https://askubuntu.com/questions/895733/copying-files-to-a-usb-drive](https://askubuntu.com/questions/895733/copying-files-to-a-usb-drive)
* Install network manager without internet  
  * [https://askubuntu.com/questions/422928/how-to-reinstall-network-manager-without-internet-access](https://askubuntu.com/questions/422928/how-to-reinstall-network-manager-without-internet-access)
* When server stops working follow my reddit post  
  * [https://www.reddit.com/r/HomeServer/comments/1bfi2u2/server\_in\_local\_network\_is\_inaccessible\_cannot/](https://www.reddit.com/r/HomeServer/comments/1bfi2u2/server_in_local_network_is_inaccessible_cannot/)

## Ubuntu laptop would not connect to shared drive using smb protocol

* Issue: as soon as you wrote `smb:` it turns red in file explorer `other locations > enter server address`
  * following library may have been deleted during some upgrade or autoremove
  * Run this command `sudo apt install gvfs-backends`
  * [Forum link where I found the resolution](https://ubuntuforums.org/showthread.php?t=2471298)