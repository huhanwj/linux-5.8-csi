# linux-5.12-csi
This project aims to make the Atheros CSI Tool developed by Wirless And Networked Distributed Sensing (WANDS) system group @ NTU, Singapore work on newer linux kernel (i.e. 5.12 in our project).

## Notice for downloading this repository

Do NOT try to clone or download the ZIP file and unzip it under Windows Environment (Chinese Lang.), it will raise an directory error (unclear about the detailed reason but I guess is related to encoding schemes as I am using a Chinese lang version of Windows).

All of our testing is done on x86 platforms, we don't know whether this is compatible with ARM chips.

Also Github currently does not accept account passwords to authenticate Git operations, you may use SSH clone instead of HTTPS clone.

## Installation
**First, remember to download or clone the whole repository.**

### System Requirements
Any Ubuntu system (we only test on Ubuntu machines)

### Install required packages
Some packages are needed (may still have missing packages when compiling, add the missing packages yourself depending on what error you encounter)

`sudo apt-get install build-essential bison bc flex libncurses5-dev libncursesw5-dev libssl-dev libelf-dev`

Then, run the following command in this folder

`make menuconfig`

Make sure that the items under *Atheros 802.11n wireless cards support* in `Device Drivers > Network device support > Wireless LAN` is enabled (enabling by space key). Save first and then exit.

Next compile the kernel modules

```bash
make -j<n>
make modules
sudo make modules_install
sudo make install
```

Note here that the `-j<n>` is used for accelerating the compiling process. The number n is select according to the number of threads that your CPU have. If your CPU has hyperthreading technology (HT), the number should be 2 times your CPU cores (e.g. most Intel Core i7/i9 CPUs, Intel Xeon CPUs and AMD Ryzen/ThreadRipper CPUs). For CPUs not supporting such technology, which normally depends on the settings of chip manufacturer (e.g. i7-9700K does not support HT but i7-8700K does), just put in the number of your CPU cores (e.g. the CPUs used for my testing, which are Intel Core i5-4590T and Intel Core i5-9600K).

## Notice for building

Do NOT put the folder under some folder with space in its name like Untitled folder, it will result in a make error during the `sudo make modules_install`.

If you find that uname -r does not give 5.12.0+, then you can modify `/etc/default/grub` and deactivate `GRUB_HIDDEN_TIMEOUT=0` by commenting it. Then run `sudo update-grub` to update the grub and reboot the system. You can see the grub menu and select advanced options for ubuntu and select our customized kernel.