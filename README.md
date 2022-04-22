# ubuntu18_newest_hardware
Instruction for installing and setup ubuntu 18.04 for newest hardware

## Installing UBUNTU 18.04 in newest hardware(for me is GIGABYTE YE5 RTX 3080 Ti)

### Problem:
The lastest kernel version for ubuntu 18.04 is 5.4.*(for now: 189)
But it does not support Intel 12th-gen chipset and iGPU.

In this case, if you try to install nvidia-driver-510, then it seems like successfully installed.
But if you

    nvidia-smi

in terminal then you can see only /usr/lib/xorg/Xorg.

I means that application on your computer can not use graphics card because kernel cannot detect newest hardware RTX 3080 Ti.
If correctly installed, also /usr/bin/gnome-shell should be shown in nvidia-smi


Furthermore, many newest hardware(ex: WiFi-6 NIC, Trackpad, Webcam, Bluetooth module) is unable to use in present kernel versions for bionic.


### Solution:
Try install higher version of kernel for Ubuntu bionic(18) first. For now official canonical version 5.4.* does not support our hardware.
So we have to choose alternative way.

Install bionic capable custom Kernel update.
Now, Kernel 5.17-8ubuntu1~bionic is available in liquorix.
Please refer https://liquorix.net .


*If you already installed nvidia-driver-510, you can let driver installed and just install newest kernel.
*You don't have to uninstall before updating kernel.


    sudo add-apt-repository ppa:damentz/liquorix
    sudo apt-get update


and if you are in x64-based computer

    sudo apt-get install linux-image-liquorix-amd64 linux-headers-liquorix-amd64

if not follow instructions in https://launchpad.net/~damentz/+archive/ubuntu/liquorix.


and reboot then,
you can see 
/usr/bin/gnome-shell in nvidia-smi
and also, many hardware is now available in your computer!

Enjoy!


*I think it will works for not only Bionic but also ubuntu focal(20.04), ubuntu hirsute(21.04), ubuntu impish(21.10).
*If you have trouble in installing NVIDIA driver for old Ubuntu just try and please leave a comment it works or not.
