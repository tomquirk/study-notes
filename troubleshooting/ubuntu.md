# Ubuntu guidez

## "stuck of fsck (x/y blocks) on boot"

1. restart
1. Immediately after BIOS screen, press `ESC` ONCE. You should see a selection page with purple bkgrnd (pressing multiple times might land you immediately to the GRUB CLI)
1. set `nomodeset` (like [here](https://askubuntu.com/questions/38780/how-do-i-set-nomodeset-after-ive-already-installed-ubuntu))
1. reboot. Hopefully this gets us to login page
1. Log in (or get access to a terminal somewhow)
1. 
```
$ sudo apt remove --purge nvidia*
$ sudo apt autoremove
```
1. Go to "Software & Updates" application, to the "Other Software" tab and remove any `ppa` stuff
1. reboot
1. 
```
$ sudo apt update && sudo apt upgrade
```
1. Install the nvidia stuff by using [this](https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-18-04-bionic-beaver-linux) guide (the "Automatic Install using standard Ubuntu Repository" option"
1. 
```
$ sudo apt update && sudo apt upgrade
```
1. Reboot
1. Test