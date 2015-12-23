## Setup for development environment
* Dual boot OS X with ubuntu 14.04 on a macbook pro 11,3
* 14.10, 15.04, and 15.10 have all worked when starting from scratch, but upgrading between them proves difficult

### Things that consistently don't work
1. Webcam
2. Graphics card switching (supposedly is possible to swap on boot, but I just stick to nvidia card)
3. Suspend/resume sorta works but not reliable

### Partition and Installation
1. Create partition for OS X from disk utility
2. Create shared partition if desired, using HFS non-journaled
3. Install yosemite in its partition
4. Install any OS X upgrades before doing linux stuff
5. Install rEFInd
6. Unetbootin to create ubuntu live usb
7. Live usb won't detect yosemite partition, so manually create install partition at / and also a swap partition

### Ubuntu important setup
1. Install wifi drivers (with dpkg or gui)
  * pool/main/d/dkms
  * pool/restricted/b/
2. Install nvidia drivers via additional drivers. 352.63 works fine, remember it being way more finicky last time
3. Screen brightness keys dont work under nvidia drivers
  * add "setpci -v -H1 -s 00:01.00 BRIDGE_CONTROL=0" to /etc/rc.local
4. Set up access for shared HFS partitions
  * sudo apt-get install hfsprogs
  * sudo fsck.hfsplus -f /dev/sdXY
  

### Ubuntu not-so-important stuff
1. Swap alt and command and add right ctrl with 
  * xmodmap swapAltCommand
2. Install xdotool and hook up raiseterminal.sh to replace ctrl-alt-T
3. Disable mouse acceleration
  * xset m 1 1

### Ubuntu even-less-important stuff
1. Turn off suspend/hibernate things
2. Turn off sticky edges in displays
3. Move menus to windows in appearance->behavior

### Emacs prerequisites
1. Get latest release
2. Install emacs dependencies
  * sudo apt-get build-dep emacs24
3. For magit, need latest git
  * sudo add-apt-repository ppa:git-core/ppa

### Emacs Irony / Rtags setup
1. Export compile commands for projects
  * -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
2. Install dependencies
  * sudo apt-get install libclang-3.5-dev llvm-3.5
3. Setup irony
  * M-x irony-install-server
  * M-x irony-cdb-json-add-compile-commands-path
4. Setup rtags
  * git clone --recursive https://github.com/Andersbakken/rtags.git
  * rdm &
  * rc -J compile_commands.json
