Broadcom-sta linux drivers (x64) working on 3.17 kernel!
===============================================================

Already patched for kernel 3.17 (and probably others).

Just be sure to enable CFG80211 as module, and disable kernel debugging (in kernel hacking) when compile the kernel.

I've used Krejzi (great) patches form https://aur.archlinux.org/packages/broadcom-wl/
Also includes the complied module.

Installation:
============
Check to see if ssb, bcma, wl or b43 is loaded:
# lsmod | grep "brcmsmac\|ssb\|wl\|b43\|bcma"

If any of these are installed, remove them:
# rmmod brcmsmac
# rmmod ssb
# rmmod bcma
# rmmod wl
# insmod wl

Then run:
make
modprobe lib80211
modprobe cfg80211
insmod wl.ko

Now if you run iwconfig should see the new network, if everything works fine remove the previously added module:
rmmod wl.ko 

To always load it at boot time, do:
cp wl.ko /lib/modules/`uname -r`/kernel/drivers/net/wireless 
depmod -a
echo modeprobe wl >> /etc/rc.local

If you are using Ubuntu, you should remove the included wl.ko:
sh: for i in `find /lib /var -name wl\.ko`; do mv $i ${i}.orig; done

Hope this works for you!
Regards,
Luis

