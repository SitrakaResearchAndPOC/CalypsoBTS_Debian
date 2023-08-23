# CalypsoBTS_Debian
## Demonstration : 
* [demos](https://youtu.be/_nGVeG_76W8)
## OS : 
* Debian 13.x (possible avec debin 10.x)
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
## Installation of osmocom-bb
```
git clone git://git.osmocom.org/osmocom-bb.git
```
```
cd osmocom-bb/
```
```
git checkout 4f677e6ba8434dab376495cd996d140548fa6e93
```
```
cd src
```
```
nano target/firmware/Makefile
```
"#uncomment CFLAGS += -DCONFIG_TX_ENABLE in the file target/firmware/Makefile"  
#ctrl+o return ctrl+x

```
make -j4 -e CROSS_TOOL_PREFIX=arm-none-eabi-
```
```
cd ../..
```
## Installation of libosmo-dsp
```
git clone git://git.osmocom.org/libosmo-dsp.git
```
```
cd libosmo-dsp/
```
```
git checkout 551b9752bcd5d3d21bb2df0736b1801bda3d0d10
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
## Installation of trx
```
git clone git://git.osmocom.org/osmocom-bb.git -b fixeria/trx trx
```
```
cd trx/src/
```
```
git checkout 620fe497efa492feff4550e336cc3f8167715936
```
```
nano target/firmware/Makefile
```
#uncomment CFLAGS += -DCONFIG_TX_ENABLE  
#ctrl+o return ctrl+x
```
make -j4 HOST_layer23_CONFARGS=--enable-transceiver -e CROSS_TOOL_PREFIX=arm-none-eabi-
```
```
cd ../..
```
## Installation of libosmo-abis
```
git clone git://git.osmocom.org/libosmo-abis.git
```
```
cd libosmo-abis/
```
```
git checkout 39dffb6c29a8d78ba8527aa4ccc13f34d1c3b319
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
ldconfig
```
```
cd ..
```
## Installation of libosmo-netif
```
git clone git://git.osmocom.org/libosmo-netif.git
```
```
cd libosmo-netif/
```
```
git checkout 09c71b04f5a8d82515d0d4d541b8368b585dbd31
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
ldconfig
```
```
cd ..
```

## Installation of openbsc
```
git clone git://git.osmocom.org/openbsc.git
```
```
cd openbsc/openbsc/
```
```
git checkout d2550da76f9974bb1957f74c5d3eb75fdae923d9
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
ldconfig
```
```
cd ../..
```
## Installation of osmo-bts
```
git clone git://git.osmocom.org/osmo-bts.git
```
```
cd osmo-bts/
```
```
git checkout 59e7773055335a12d749faf84d88a8ed9fa0f201
```
```
autoreconf -i
```
```
./configure --enable-trx
```
```
make -j4
```
```
make install
```
```
ldconfig
```
```
cd ..
```
## Testing shell 0
```
cd /home/debian/osmocom/trx/src/ && \
host/osmocon/osmocon -m c123xor -p /dev/ttyUSBX -c target/firmware/board/compal_e88/rssi.highram.bin
```
##
## Finding phone
```
dmesg | grep tty
```
##
## shell 1
* With two phones : 
```
cd /home/debian/osmocom/trx/src/ && 
host/osmocon/osmocon -m c123xor -p /dev/ttyUSBX -s /tmp/osmocom_l2 -c target/firmware/board/compal_e88/trx.highram.bin
```
Please replace X on /dev/ttyUSBX  with correct number and push power button of motorola phone 1
* With only one phone : 
```
cd /home/debian/osmocom/trx/src/ && 
host/osmocon/osmocon -m c123xor -p /dev/ttyUSB0 -c target/firmware/board/compal_e88/trx.highram.bin
```
Please replace X on /dev/ttyUSBX  with correct number and push power button of motorola phone
##
## shell 2
* With two phones :
```
cd /home/debian/osmocom/trx/src/ && \
host/osmocon/osmocon -m c123xor -p /dev/ttyUSBX -s /tmp/osmocom_l2.2 -c target/firmware/board/compal_e88/trx.highram.bin
```
Please replace X on /dev/ttyUSBX  with correct number and push power button of motorola phone 2

* With one phone :
 No command
##
## shell 3
* With two phones : 
```
cd /home/debian/osmocom/trx/src/host/layer23/src/transceiver/ && \
./transceiver -a X -2
```
* With one phone :
```
./transceiver -a X 
```
##
## Before launching next shell, preparing configs
* config file of osmo-bts
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/CalypsoBTS_Debian/main/osmo-bts.cfg
``` 
* config file of open-bsc
``` 
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/CalypsoBTS_Debian/main/open-bsc.cfg
``` 
* config  hlr.sqlite3
```
touch hlr.sqlite3
```
##
## shell 4
```
osmo-nitb -c open-bsc.cfg -l hlr.sqlite3 -P -C --debug=DRLL:DCC:DMM:DRR:DRSL:DNM
```
##
## shell 5
```
osmo-bts-trx -c osmo-bts.cfg --debug DRSL:DOML:DLAPDM
```
##
## Code for managing BTS
```
telnet localhost 4242
```
```
telnet localhost 4241
```
##
## Code getting number MSISDN or extension on the network
```
*#100#
```
















