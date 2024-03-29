# ubuntu18_newest_hardware
Instruction for installing and setup ubuntu 18.04 for newest hardware

## Installing UBUNTU 18.04 in newest hardware(for me is GIGABYTE YE5 RTX 3080 Ti and DDR5 mainboard, RTX3090, RTX A6000)

### Problem:
The latest kernel version for Ubuntu 18.04 is 5.4.*(for now: 189)
But it does not support Intel 12th-gen chipset and iGPU.

In this case, if you try to install nvidia-driver-510, then it seems like successfully installed.
But if you

    nvidia-smi

in terminal then you can see only /usr/lib/xorg/Xorg.

It means that application on your computer can not use a graphics card because the kernel cannot detect the newest hardware RTX 3080 Ti.
If correctly installed, also /usr/bin/gnome-shell should be shown in nvidia-smi


Furthermore, many newest hardware(ex: WiFi-6 NIC, Trackpad, Webcam, Bluetooth module) is unable to use in present kernel versions for bionic.


### Solution:
Try install a higher version of kernel for Ubuntu bionic(18) first. For now official canonical version 5.4.* does not support our hardware.
So we have to choose the alternative way.

Install bionic capable custom Kernel update.
Now, Kernel 5.17-8ubuntu1~bionic is available in Liquorix.
Please refer https://liquorix.net .


*If you already installed nvidia-driver-510 on your computer, you can let driver be installed and can just install the newest kernel.
*You don't have to uninstall before updating the kernel.


    sudo add-apt-repository ppa:damentz/liquorix
    sudo apt-get update


and if you are in x64-based computer,

    sudo apt-get install linux-image-liquorix-amd64 linux-headers-liquorix-amd64

If not follow instructions in https://launchpad.net/~damentz/+archive/ubuntu/liquorix.


and reboot then,
you can see 
/usr/bin/gnome-shell in nvidia-smi
and also, many hardware is now available in your computer!

Enjoy!

#### If the desktop does not appear after installing the kernel and rebooting,
then try booting with an older version of the kernel in an advanced setup on grub.
And re-install the nvidia-driver by following nvidia installation manual.


*I think it will works for not only Bionic but also ubuntu focal(20.04), ubuntu hirsute(21.04), ubuntu impish(21.10).
*If you have trouble in installing NVIDIA driver for old Ubuntu just try and please leave a comment it works or not.


### If the computer bootup directly with Windows without showing a grub screen
While booting procedure, click del key to enter BIOS setup.
And set Ubuntu higher than Winodws in booting priority. Please double-check not only the GUI interface in BIOS but also the detailed settings in boot menu.

### If you facing the "bad shim signature" while booting
Go to the BIOS and disable the "SECURE BOOT" option.
Or if there is no secure boot option, then find "Delete all secure boot variables" and confirm it.

### Install WiFi6 (AX210) Driver

    sudo apt update
    sudo apt-get install -y git
    sudo apt-get install -y build-essential

    git clone git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
    cd linux-firmware
    sudo cp iwlwifi-* /lib/firmware/
    cd ..

    git clone https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git
    cd backport-iwlwifi
    make defconfig-iwlwifi-public
    make -j4
    sudo make install
 
    sudo update-initramfs -u
    sudo reboot

## Setting NVIDIA Driver and CUDA

### Uninstall pre-existing NVIDIA DRIVER

    sudo apt-get purge nvidia*
    sudo apt-get autoremove
    sudo apt-get autoclean
   
#### Remove CUDA cleanly

    sudo rm -rf /usr/local/cuda*
    sudo apt-get --purge remove 'cuda*'
    sudo apt-get autoremove --purge 'cuda*'
    
#### Check if ALL drivers and CUDA are uninstalled and removed, if not clean remove

    sudo dpkg -l | grep nvidia
    
if something remains,

    sudo apt-get remove --purge [name of package]
    
for all remain packages

    sudo dpkg-l | grep cuda
    
if something remains,

    sudo apt-get remove --purge [name of package]
    
### Install new nvidia driver

    sudo apt-get update
    sudo apt-get install nvidia-driver-510


