# linux-5.8-csi
This project aims to make the Atheros CSI Tool developed by Wirless And Networked Distributed Sensing (WANDS) system group @ NTU, Singapore work on newer linux kernel (i.e. 5.8 backport in our project).

## Notice for downloading this repository

Do NOT try to clone or download the ZIP file and unzip it under Windows Environment (Chinese Lang.), it will raise an directory error (unclear about the detailed reason but I guess is related to encoding schemes as I am using a Chinese lang version of Windows).

All of our testing is done on x86 platforms, we don't know whether this is compatible with ARM chips.

Also Github currently does not accept account passwords to authenticate Git operations, you may use SSH clone instead of HTTPS clone.

## Installation
**First, remember to download or clone the whole repository.**

### System Requirements
Any Ubuntu system with kernel version smaller or equal to 5.8(we only test on Ubuntu machines)

For Ubuntu 18.04, please use 5.8 backport

For Ubuntu 16.04, please use 4.19 backport

### Install required packages
Some packages are needed (may still have missing packages when compiling, add the missing packages yourself depending on what error you encounter)

`sudo apt-get install build-essential bison bc flex libncurses5-dev libncursesw5-dev libssl-dev libelf-dev`

First, you should go into the backport version that you'd like to install, i.e. `cd backport-5.8-1`

Then, run the following command in this folder

`make defconfig-ath9k`

Next compile the kernel modules

```bash
make -j<n>
sudo make install
```

Note here that the `-j<n>` is used for accelerating the compiling process. The number n is select according to the number of threads that your CPU have. If your CPU has hyperthreading technology (HT), the number should be 2 times your CPU cores (e.g. most Intel Core i7/i9 CPUs, Intel Xeon CPUs and AMD Ryzen/ThreadRipper CPUs). For CPUs not supporting such technology, which normally depends on the settings of chip manufacturer (e.g. i7-9700K does not support HT but i7-8700K does), just put in the number of your CPU cores (e.g. the CPUs used for my testing, which are Intel Core i5-4590T and Intel Core i5-9600K).

Finally, reboot the system to make it work.

## Conf
For Conf, please see the [wiki](https://github.com/huhanwj/linux-5.8-csi/wiki) page

## UserSpace tool
For hostapd conf, please also refer to the [wiki](https://github.com/huhanwj/linux-5.8-csi/wiki) page.

For other tools, we use the same one as provided in original CSI tool.

## Source

*Source code of Atheros CSI Tool*: https://github.com/xieyaxiongfly/Atheros-CSI-Tool

*Manual for Atheros CSI Tool*: https://wands.sg/research/wifi/AtherosCSI/document/Atheros-CSI-Tool-User-Guide.pdf
