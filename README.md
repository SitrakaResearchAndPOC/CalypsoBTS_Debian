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
## Installation of dependencies
```
apt update
```
```
sudo apt-get install libtool shtool automake dahdi-source libssl-dev sqlite3 libsqlite3-dev libsctp-dev libfftw3-dev libfftw3-3 autoconf libsctp-dev libgnutls28-dev libcurl4-gnutls-dev git-core pkg-config make gcc gcc-arm-none-eabi doxygen libtalloc-dev libpcsclite-dev libusb-1.0-0-dev
```
```
sudo apt install autoconf automake build-essential ccache cmake cpufrequtils doxygen ethtool g++ git inetutils-tools libboost-all-dev libncurses5 libncurses5-dev libusb-1.0-0 libusb-1.0-0-dev libusb-dev python3-dev python3-mako python3-numpy python3-requests python3-scipy python3-setuptools python3-ruamel.yaml
```
## Creation of repository osmocom
```
mkdir osmocom
```
```
cd osmocom
```
## Installation of libosmocore
```
git clone git://git.osmocom.org/libosmocore.git
```
```
cd libosmocore/
```
```
git checkout cf70aa0c40c574c32b832454f725cc37459c5d8d
```
```
autoreconf -i
```
```
./configure
```
```
make -j4
```
```
make install
```
```
ldconfig -i
```
```
cd .. 
```



