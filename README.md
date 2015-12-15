notes for dual boot yosemite with ubuntu 14.04 on a macbook pro 11,3
14.10 and 15.04 both work as well (with some tweaks), but had to stick to same kernel else unity would freeze and/or keyboard/mouse unresponsive.
15.10 blew everything up which is why I'm starting over again and finally listing steps this time

### Things that don't work as far as i know
1. webcam
2. suspend/resume sorta works but not reliable
3. graphics card switching (supposedly is possible to swap on boot, but i just stick to nvidia card)

### Partition and Installation
1. install yosemite in its partition
2. install rEFInd
3. unetbootin to create ubuntu live usb
4. live usb won't detect yosemite partition, so manually create install partition at / and also a swap partition

### Ubuntu important setup
1. Install wifi drivers (with dpkg or gui)
2. Install nvidia drivers via additional drivers. 352.63 works fine, remember it being way more finicky last time
3. screen brightness keys dont work under nvidia drivers
  * add "setpci -v -H1 -s 00:01.00 BRIDGE_CONTROL=0" to /etc/rc.local

### Ubuntu not-so-important stuff
1. Swap alt and command and add right ctrl with 
  * xmodmap swapAltCommand
2. Install xdotool and hook up raiseterminal.sh to replace ctrl-alt-T
3. Disable mouse acceleration
  * xset m 0 0

### Ubuntu even-less-important stuff
1. Turn off suspend/hibernate things
2. Turn off sticky edges in displays
3. Move menus to windows in appearance->behavior

### Emacs prerequisites
1. Get latest release
2. Install emacs dependencies
  * sudo apt-get build-dep emacs24
3. for magit, need latest git
  * sudo add-apt-repository ppa:git-core/ppa
