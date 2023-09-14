#!/bin/bash

# Step 1: Update from the existing repositories =============================================

sudo dnf upgrade

sleep 5; clear

# Step 2: Add the RPMFusion repository for NVIDIA drivers =============================================

sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

sleep 5; clear

# Step 3 Update from the newly added repositories =============================================

sudo dnf upgrade --refresh

sleep 5; clear

# Step 4: Install the driver and its dependencies =============================================

sudo dnf install gcc kernel-headers kernel-devel akmod-nvidia xorg-x11-drv-nvidia xorg-x11-drv-nvidia-libs xorg-x11-drv-nvidia-libs.i686

sleep 5; clear

# Step 5: Wait for the kernel modules to load up =============================================

echo -e "You must wait 5 minutes for the kernel modules to load.\n\033[0;31mPlease do not proceed to the next steps immediately\033[0m"
 hour=0
 min=5
 sec=3
        while [ $hour -ge 0 ]; do
                 while [ $min -ge 0 ]; do
                         while [ $sec -ge 0 ]; do

                                 echo -ne "\033[1;34m$hour:$min:$sec\033[0K\r"
                                 let "sec=sec-1"
                                 sleep 1
                         done
                         sec=59
                         let "min=min-1"
                 done
                 min=59
                 let "hour=hour-1"
         done
          
echo -ne "The countdown is over, next step will start shortly"

sleep 20; clear

# Step 6: Read from the updated kernel modules =============================================
echo "Kernel modules update process, please wait"

sudo akmods --force && sudo dracut --force

sleep 5; clear

# Step 6: Reboot your system =============================================

echo -e "Wait for 5 minutes for the changes to take effect. Script will reboot system automatically after this time"
 hour=0
 min=5
 sec=0
        while [ $hour -ge 0 ]; do
                 while [ $min -ge 0 ]; do
                         while [ $sec -ge 0 ]; do

                                 echo -ne "\033[1;34m$hour:$min:$sec\033[0K\r"
                                 let "sec=sec-1"
                                 sleep 1
                         done
                         sec=59
                         let "min=min-1"
                 done
                 min=59
                 let "hour=hour-1"
         done
          
echo -ne "The countdown is over, system will be reboot shortly"
sleep 20

sudo reboot
