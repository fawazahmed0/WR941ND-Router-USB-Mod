# wr941nd-usb-mod using openwrt
TP-Link wr941nd V3 USB Mod

By attaching usb in your router you can torrent in your router,setup NAS in your router,install software/packages in router and many more things

## Hardware Modification Part:







Things Required: 

- 15k ohm resistor SMD, 2 Pieces 
- 4.7k ohm resistor SMD, 1 Piece
- 22 ohms resistors SMD ,2 Pieces
- USB female connector
- Wires
- Soldering iron and Solder
- 7805 voltage regulator (Optional, if you can supply external
5volts to USB)
- 470uf 16v cap regulator ,2 Pieces (Optional. only if you are
not buying 7805)

Attach 4.7k ohm resistor as shown in figures

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/a_4.7k_resistor1.jpg)



Attach 15k ohm resistor as shown in figures

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/b_15k_resistor2.jpg)
![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/c_15k_resistor1.jpg)
![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/d_15k_resistor2.jpg)


Attach 22 ohms resistor as shown in figures

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/e_22_ohm_resistor1.jpg)
![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/f-22-ohm-resistor2.jpg)











USB connector and board connection

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/g-usb-location-in-board.jpg)





5volts for USB Connector

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/h-flow.png)

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/i_9volts.jpg)

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/i-negative.jpg)







My router pictures


![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/io_end.jpg)

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/ip_end.jpg)



## Software part





Note: If your router version is 3 i.e. same as mine, you can
use my firmware instead of going through whole compilation process







You should have Linux system, I used Ubuntu on VMware



Setup



Refer 
https://wiki.openwrt.org/doc/howto/buildroot.exigence
https://wiki.openwrt.org/doc/howto/build





Open Terminal and paste each one by one





`sudo apt-get update`





`sudo apt-get install git-core build-essential libssl-dev
libncurses5-dev unzip gawk zlib1g-dev`



 



`sudo apt-get install subversion mercurial quilt`



 



`sudo apt-get install asciidoc bash bc binutils bzip2 fastjar
flex git-core gcc-c gcc util-linux gawk libgtk2.0-dev intltool jikespg
zlib1g-dev make genisoimage libncurses5-dev libssl-dev patch perl-modules
python2.6-dev rsync ruby sdcc unzip wget gettext xsltproc zlib1g-dev
libboost1.55-dev libxml-parser-perl libusb-dev bin86 bcc sharutils
openjdk-7-jdk`



 



`sudo apt-get install build-essential subversion git-core
libncurses5-dev zlib1g-dev gawk flex quilt libssl-dev xsltproc
libxml-parser-perl mercurial bzr ecj cvs unzip`



 



`sudo apt-get install build-essential subversion
libncurses5-dev zlib1g-dev gawk gcc-multilib flex git-core gettext libssl-dev`



 



`git config --global http.postBuffer 1048576000`



 



`git clone https://github.com/openwrt/openwrt.git`



`cd openwrt`



`./scripts/feeds update -a`



`./scripts/feeds install -a`



 



`make menuconfig`

















