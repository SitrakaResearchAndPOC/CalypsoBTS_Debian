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

```
#

# deb cdrom:[Debian GNU/Linux 10.13.0 _Buster_ - Official amd64 DVD Binary-1 20220910-18:04]/ buster contrib main

#deb cdrom:[Debian GNU/Linux 10.13.0 _Buster_ - Official amd64 DVD Binary-1 20220910-18:04]/ buster contrib main

# Line commented out by installer because it failed to verify:
#deb http://security.debian.org/debian-security buster/updates main contrib
# Line commented out by installer because it failed to verify:
#deb-src http://security.debian.org/debian-security buster/updates main contrib

# buster-updates, previously known as 'volatile'
# A network mirror was not selected during install.  The following entries
# are provided as examples, but you should amend them as appropriate
# for your mirror of choice.
#
 deb http://deb.debian.org/debian/ buster main contrib
 deb-src http://deb.debian.org/debian/ buster main contrib
```


