# CalypsoBTS_Debian
## Demonstration : 
* [demos](https://youtu.be/_nGVeG_76W8)
## OS : 
* Debian 10.x (possible avec debin 8.x)
* GUI choice Gnome

## Remark :
* Name of system should be : debian
## Configuration sudo su : 
* [conf_sudo_su](https://www.cyberithub.com/solved-user-is-not-in-the-sudoers-file-this-incident-reported/)
```
su root
```
```
nano /etc/sudoers
```
## Add down the text : root ALL=(ALL:ALL) ALL
```
debian ALL=(ALL:ALL) ALL
```
## Installation inspiration : 
* [inspiration](https://pastebin.com/Gi9jx6Tz)
## Change sourcelist in /etc/apt/source.list (open with gedit on interface gnome) as :

