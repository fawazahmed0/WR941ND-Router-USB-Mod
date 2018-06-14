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

- Attach 4.7k ohm resistor as shown in figures

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/a_4.7k_resistor1.jpg)



- Attach 15k ohm resistor as shown in figures

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/b_15k_resistor2.jpg)
![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/c_15k_resistor1.jpg)
![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/d_15k_resistor2.jpg)


- Attach 22 ohms resistor as shown in figures

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/e_22_ohm_resistor1.jpg)
![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/f-22-ohm-resistor2.jpg)











- USB connector and board connection

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/g-usb-location-in-board.jpg)





- 5volts for USB Connector

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/h-flow.png)

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/i_9volts.jpg)

![image](https://github.com/fawazahmed0/wr941nd-router-usb-mod/blob/master/images/i-negative.jpg)







- My router pictures


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





Open Terminal and paste & press enter each one by one





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





Now choose the options and packages you want in the menu by
pressing y or m



 



 



`make V=s -j1  `  



 



if there is error use above command again



Patch creating:



Refer: https://wiki.openwrt.org/doc/devel/patches



Open new terminal and type



 



 


```
cat > ~/.quiltrc <<EOF



QUILT_DIFF_ARGS="--no-timestamps --no-index -p ab
--color=auto"



QUILT_REFRESH_ARGS="--no-timestamps --no-index -p
ab"



QUILT_PATCH_OPTS="--unified"



QUILT_DIFF_OPTS="-p"



EDITOR="nano"



EOF

```


 



 



`cd openwrt  `  



`make target/linux/{clean,prepare} V=s QUILT=1`



Now go to
`openwrt/build_dir/target-mip-***/linux-ar71xx_generic/linux****/`



And note down the link and use it in below command.



 



`cd build_dir/target-mip-****/linux-ar71xx_generic/linux-****/`



`quilt push -a`



 



Now go to `openwrt/target/linux/ar71xx/patches****`



And note down the last file number in my case 902



Now type 



`quilt new platform/903-add-usb-wr941nd-barrierbreaker.patch`



 



Now you have to add the following changes using quilt edit



In `arch/mips/ath79/Kconfig file`



 



1.Add    



`select ATH79_DEV_USB`



Below 



`select ATH79_DEV_M25P80`



 



In `arch/mips/ath79/mach-tl-wr941nd.c`



 



1. Add



`#include <linux/gpio.h>`



below



`#include <linux/platform_device.h>`



 



2. Add



`#include "dev-usb.h"`



below



 



`#include "machtypes.h"`



 



3. Add



`#define TL_WR941ND_GPIO_USB_POWER       6`



below



`#define TL_WR941ND_GPIO_BTN_QSS                  7`



 



4. Add



```
static void __init tl_wr941nd_usb_setup(void)



{



                /*
enable power for the USB port */



                gpio_request(TL_WR941ND_GPIO_USB_POWER,
"USB power");



                gpio_direction_output(TL_WR941ND_GPIO_USB_POWER,
1);



 



                ath79_register_usb();



}

```

 



 



Below


```

                .chip                      =
&tl_wr941nd_dsa_chip,



 };
 
```


 



5. Add



`tl_wr941nd_usb_setup();`



above



`ath79_register_mdio(0, 0x0);`



 



In `/arch/mips/ath79/setup.c`



Add



`ath79_pll_wr(0x08, 0x00001030);`



below



`ath79_detect_sys_type();`



 



Refer Patch file to understand



 



Type 



`quilt edit arch/mips/ath79/Kconfig`



and do the above changes and 



do similar to other files using



`quilt edit arch/mips/ath79/mach-tl-wr941nd.c`



`quilt edit /arch/mips/ath79/setup.c`



 



When editing Choose easiest one ,the editor will get opened
up,use Ctrl+alphabet to use the options given below.Edit the file,the way you
want ,then press Ctrl+X(i.e Exit in options)



press y to save it and enter to save the file with name



 



After editing type



`quilt diff `



to see differences,type q at END



 



`quilt refresh`



 



Now the patch is saved at 



`openwrt/build_dir/target-mips****2/linux-ar71xx_generic/linux***/patches/platform`



 



Open new terminal and type



`cd openwrt`



`make target/linux/update V=s`



`make target/linux/{clean,prepare} V=s QUILT=1`



If the above command throw error then you have to edit the
patch again



 



Now go to `openwrt/target/linux/ar71xx/patches-***` and check
if your patch is there not



If not there then go to `openwrt/build_dir/target-mips****2/linux-ar71xx_generic/linux***/patches/platform`



And copy your patch and paste it at `openwrt/target/linux/ar71xx/patches-***`



 



`make clean`



`make V=s -j1`



 



Done



You can find the firmware images at bin folder



 



Flash the firmware in your router and install packages
related to usb such as block-mount



```

kmod-scsi-core

kmod-fs-ext4

kmod-usb-storage

kmod-usb-storage-extras

kmod-usb2

kmod-usb-uhci

kmod-usb-ohci

```



 



 



 



Now format your usb device as ext4 and attach to router



 



You can check whether usb is detected or not by seeing log.



It should show something like this


```
[    7.200000] scsi
0:0:0:0: Direct-Access     SanDisk  Cruzer Edge      2.01 PQ: 0 ANSI: 6

[    7.210000] sd
0:0:0:0: [sda] 15633408 512-byte logical blocks: (8.00 GB/7.45 GiB)

[    7.230000] sd
0:0:0:0: [sda] Write Protect is off

[    7.230000] sd
0:0:0:0: [sda] Mode Sense: 43 00 00 00

[    7.240000] sd
0:0:0:0: [sda] Write cache: disabled, read cache: enabled, doesn't support DPO
or FUA


```

 



Now mount the usb as exroot to increase space



Refer https://wiki.openwrt.org/doc/howto/extroot



Refer openwrt docs for more help



 



 



















