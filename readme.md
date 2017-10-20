Zcash miner under linux manjaro with GTX1080

Prepare:
1. GTX1080,
2. X86 PC support 64bit ,4G memory,250Gb Sata HDD
3. Usb stick above 2G bytes


Step1:
Download manjaro image, there are three version, I like gnome style ,so I take it
Gnome: https://downloads.sourceforge.net/manjarolinux/manjaro-gnome-17.0.5-stable-x86_64.iso
KDE: https://downloads.sourceforge.net/manjarolinux/manjaro-kde-17.0.5-stable-x86_64.iso
Xfce:https://downloads.sourceforge.net/manjarolinux/manjaro-xfce-17.0.5-stable-x86_64.iso


Step2:
Burn manjaro image to USB stick
linux:
To burn the iso on an usb stick, enter the following command in a terminal : 
$sudo dd bs=4M if=/path/to/manjaro.iso of=/dev/sd[drive letter] status=progress

windows:use imagewriter
https://launchpad.net/win32-image-writer/

Step3:
Install manjaro  to system by usb stick.


Step4:
Boot into system, install kernel ,kenrel header for build kernel module, cuda for miner tool

$sudo pacman -Sy
$sudo pacman -S cuda
$sudo pacman -S gcc make automake
$sudo pacman -S linux
$sudo pacman -S linux linux-headers
sudo pacman -S gcc-libs-multilib

do a reboot 
$reboot

Step5:
Boot into system , check if  system run new kernel 

$uname -a
Linux manjaro 4.9.53-1-MANJARO #1 SMP PREEMPT Thu Oct 5 15:11:15 UTC 2017 x86_64 GNU/Linux

download nvida driver 
$mkdir nv
$cd nv
$wget http://download.nvidia.com/XFree86/Linux-x86_64/384.90/NVIDIA-Linux-x86_64-384.90.run
download ewbf miner tool ,unzip miner tool
$wget https://github.com/nanopool/ewbf-miner/releases/download/v0.3.4b/Zec.miner.0.3.4b.Linux.Bin.tar.gz
$tar xvf Zec.miner.0.3.4b.Linux.Bin.tar.gz
modify start.sh , change the miner pool server ,port and miner address by gedit
$gedit start.sh

Step6:
install nvida linux driver 
$ sudo ./NVIDIA-Linux-x86_64-384.90.run
It will report an error, we should boot to text mode to install the dirver, type below command to disable gdm and reboot
$sudo systemctl disable gdm
$sudo reboot
after reboot, we goto into a ternimal,  just login and change to the nv directory, type command wait for command over.

sudo ./NVIDIA-Linux-x86_64-384.90.run

if successful , then run miner commnad 
$sudo ./start.sh
if you want to run it under gnome desktop, run comand 
$sudo systemctl enable gdm
$sudo systemctl start gdm
open a terminal 
$sudo ./start.sh

Enjoy! Below is my miner output !

Hope it can help somebody!

Accept donate 
ZEC: t1dY6yNRb8RHTmTUuyAiEEbXojfkiWPgNUF
BTC: 1Nf2QZCdsGb2giXiUZE5i4vvp5yvwXGEu2
ETH: 0x91ad2d34f03f0a8a50753bc7fc0dd4dc64454985


+-------------------------------------------------+
|         EWBF's Zcash CUDA miner. 0.3.4b         |
+-------------------------------------------------+
INFO: Current pool: cn1-zcash.flypool.org:3333
INFO: Selected pools: 1
INFO: Solver: Auto.
INFO: Devices: All.
INFO: Temperature limit: 90
INFO: Api: Disabled
---------------------------------------------------
INFO: Target: 0004189374bc6a7e...
CUDA: Device: 0 GeForce GTX 1080, 8112 MB i:64
INFO: Detected new work: 23f810c9b33017e54043
CUDA: Device: 0 Selected solver: 0
INFO: Detected new work: 7d2f3b912be7344458fb
Temp: GPU0: 83C 
GPU0: 488 Sol/s 
Total speed: 488 Sol/s
INFO 08:21:15: GPU0 Accepted share 49ms [A:1, R:0]
INFO 08:21:25: GPU0 Accepted share 53ms [A:2, R:0]



