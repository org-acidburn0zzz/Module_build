# Module_build

on Sparky (ubuntu 12.04 image) compile driver modules , steps explained below.

login as root

Download latest updates.

apt-get update

#*****************************
note: if the sd card not fully configured use parted (version 3.2) tool to resize the partition.
check df -h ,on 8GB sd card size should show above 7GB.
parted /dev/mmcblk0
(parted)resizepart 2
warning:partition /dev/mmcblk0p2 is being used. Are you sure you want to continue?
yes/No?yes
End? [7xGB]? -1
(parted)q

reboot the board and on terminal enter the command
root@sparky#resize2fs /dev/mmcblk0p2/
..
The filesystem on /dev/mmcblk0p2 is now  xxxxxx blocks long
root@sparky#df -h

#***********************************************


Download linux kernel source, this is needed to compile the driver module.

cd /usr/src
git clone https://github.com/sparkysbc/Linux.git
sudo ln -s /usr/src/Linux /lib/modules/`uname -r`/build
cd Linux

Prepare the kernel with the current kernel config from the running system
(current config available on /boot/)
make mrproper
wget https://raw.githubusercontent.com/sparkysbc/Module_build/master/.config
(current config available on /boot/)
Download the module symbols of the current kernel.
wget https://github.com/sparkysbc/Module_build/blob/master/Module.symvers
make modules_prepare

#*******************************                                                                          
