[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://paypal.me/matteoiervasi)
[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/dell-xps-9570-ubuntu-respin/Lobby?utm_source=share-link&utm_medium=link&utm_campaign=share-link)

# DELL XPS 15 9570 Ubuntu post installation script (18.04,19.04 and 19.10)

### Table of Contents
1. [Post-install script](#post-install-script)
2. [Switching from one graphic card to the other](#how-to-switch-from-one-graphic-card-to-the-other)
3. [Troubleshooting](#troubleshooting)

Collection of scripts and tweaks to make Ubuntu 18.04/19.04/19.10 run smooth on Dell XPS 15 9570.
I suggest everyone to use the post install method, the respun ISO is no longer supported nor neeeded for booting Ubuntu on 9570 as the stock one contains the needed fixes.

All informations, tips and tricks was gathered from:

- [tomwwright gist for DELL XPS 15 9560](https://gist.github.com/tomwwright/f88e2ddb344cf99f299935e1312da880)
- [Atheros wifi card fix](https://ubuntuforums.org/showthread.php?t=2323812&page=2)
- [Respin script and info](http://linuxiumcomau.blogspot.com/)
- Myself xD

Kudos and all the credits for things not related to my work go to developers and users on those pages!

### What works out-of-the-box
 - ✅ Atheros Wifi
 - ✅ Audio
 - ✅ Audio on HDMI
 - ✅ HDMI ( even on lid closed )
 - ✅ Nvidia/Intel graphic cards switch
 - ✅ Keyboard backlight
 - ✅ Display brightness
 - ✅ Sleep/wake on Intel

### What does't work properly
 - ➖ Sleep/wake on nVidia

### What doesn't work
 - ❌ Goodix Fingerprint sensor

## Post-install script
If you already have a standard Ubuntu install, you can try applying basic tweaks with the `xps-tweaks.sh` script.
You can run it directly without cloning the repository with the following command (requires `curl`):
```shell
bash -c "$(curl -fsSL https://raw.githubusercontent.com/JackHack96/dell-xps-9570-ubuntu-respin/master/xps-tweaks.sh)"
```

If you want touchpad gestures using X11, check https://github.com/bulletmark/libinput-gestures or better https://github.com/iberianpig/fusuma.

## How to switch from one graphic card to the other
Starting from nVidia 435 drivers, we can finally offload apps like on Windows without having to use very complicated setups with Bumblebee.
If during the script you chose to not enabling offloading, you can use the classic `prime-select` command:

**Intel**:
```
sudo prime-select intel
```
**Nvidia**:
```
sudo prime-select nvidia
```

**Nvidia**:
```
sudo prime-select nvidia
```

**kernel params**:
```
Kernel Boot Options:. loglevel=0 pcie_aspm=force acpi_rev_override=1 mem_sleep_default=deep acpi_osi=Linux scsi_mod.use_blk_mq=1 nouveau.modeset=0 acpi_sleep=nonvs systemd.show_status=false nouveau.runpm=0 splash quiet drm.vblankoffdelay=1 apm=on apm=power-off
```

**Note: A full reboot could be required when switching graphic cards.**

## Troubleshooting

Check the [wiki page](https://github.com/JackHack96/dell-xps-9570-ubuntu-respin/wiki/Troubleshooting) about it.

## Beautify
[mac like](https://linuxconfig.org/how-to-install-macos-theme-on-ubuntu-20-04-focal-fossa-linux)  
[Gnome login change](https://www.ostechnix.com/how-to-change-gdm-login-screen-background-in-ubuntu/)  
[theme](https://www.gnome-look.org/p/1241688/)  
[theme2](https://www.gnome-look.org/p/1275087/)  
[icon pack](https://www.gnome-look.org/p/1102582/)  
wine chinese input  
最后想到了XMODIFIERS可能跟wine输入法有关，百度找到这个网页，在终端尝试输入export XMODIFIERS=@im=ibus | notepad，结果wine终于能输入中文了！折腾两天，终于找到答案，怎不让人兴奋！  
答案：在/etc/profile的最后添加这一句： export XMODIFIERS=@im=ibus  
[Sound-fix](https://www.linuxuprising.com/2018/06/fix-no-sound-dummy-output-issue-in.html)  
[docker-fix](https://stackoverflow.com/questions/48957195/how-to-fix-docker-got-permission-denied-issue)  
[virtualbox](https://www.virtualbox.org/wiki/Download_Old_Builds_6_0)  
[k2](https://github.com/Kurgol/keychron/blob/master/k2.md)  
numlock: sudo gedit /usr/share/X11/xkb/keycodes/evdev, change NMLK to 770  
```
  #lockDialogGroup {
   background: #2c001e url(file:///home/yangl/Pictures/wallpapers/planet_earth_4k-2560x1440-blur.jpg);
   background-repeat: no-repeat; 
   background-size: cover;
   background-position: center;
}  
```
[auto-cpufreq](https://github.com/AdnanHodzic/auto-cpufreq)  
sudo apt-get install gnome-sushi  
[sof](https://www.alsa-project.org/files/pub/misc/sof/)  
Update /usr/lib/firmware/intel/sof and /usr/lib/firmware/intel/sof-tplg folder to the ones in the link above  
It seems that adding "load-module module-alsa-source device=hw:0,7" to "/etc/pulse/default.pa" i have the mic recognized and working  
[ukuu](https://frank.kumro.io/installing-a-mainline-kernel-on-popos/)  
[ukuu releases](https://github.com/teejee2008/ukuu/releases)  
[pin kernel](https://frank.kumro.io/stop-kernel-updates-on-pop-_os/)  
[ldac](https://github.com/EHfive/pulseaudio-modules-bt/issues/85#issuecomment-624503956)
