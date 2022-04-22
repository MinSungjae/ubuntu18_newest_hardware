# ubuntu18_newest_hardware
Instruction for how to install and setup ubuntu 18.04 for newest hardware

## Installing UBUNTU 18.04 in newest hardware(for me is GIGABYTE YE5 OLED with RTX 3080 Ti)

### Present problem:
The lastest kernel version for ubuntu 18.04 is 5.4.*(now: 189)
But it does not support Intel 12th gen iGPU

In this case, if you try to install nvidia-driver-510 then it seems like correctly installed.
But you can see only
/usr/lib/xorg/Xorg in nvidia-smi
because kernel cannot detect newest hardware RTX 3080 Ti
If correctly installed, also /usr/bin/gnome-shell should be shown in nvidia-smi


Furthermore, many newest hardware(ex: WiFi-6 NIC, Trackpad, Webcam, Bluetooth module) is unable to use in present kernel versions for bionic.


### Solution:
Try install higher version of kernel for Ubuntu bionic(18) first. But for now official canonical version 5.4.* does not support.
So we have to choose alternative way.

Install bionic capable custom Kernel update
Now, Kernel 5.17-8ubuntu1~bionic is available in liquorix.
Please refer https://liquorix.net


*If you already installed nvidia-driver-510, you can let driver installed and just install newest kernel.
You don't have to uninstall before updating kernel.

  sudo add-apt-repository ppa:damentz/liquorix
  sudo apt-get update

and


  sudo apt-get install linux-image-liquorix-amd64 linux-headers-liquorix-amd64



and reboot then,
you can see 
/usr/bin/gnome-shell in nvidia-smi
and also, many hardware is now available in your computer!
