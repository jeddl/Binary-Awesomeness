---
title: Manjaro - Installation and Configuration
published: true
---


I have wanted to try Arch or an Arch based Linux distro for a while. Recently I decided to give
[Manjaro](https://manjaro.org/) Architect along with [i3](https://i3wm.org/) WM a shot. (I have also tried KDE Plasma and GNOME,
but didn't quite like it as I was not trying to configure my entire Linux desktop like Mac or Windows.)

The reason why I chose Manjaro Architect with i3 was:

1. It is Arch based, and I really would like to experience one of these rolling release distros.
2. It is not Arch, which means, for example the Manjaro Architect, comes with some feature pre-installed so that I didn't
   have to start from completely scratch.(Which might be really good for those who want to start from 0. And one of the advantages of
   doing it is you will absolutely know your system inside-out)
3. i3 is fast and keyboard based, also really simple and beautiful(simple is beautiful of course), which is exactly what
   I need.

## Preparation

I have an old 2013 MacBook pro which was not really active at the moment, so I decided to give it a try regardless
the bad customization capability of Apple.

Here are some of the details of my machine

```bash
System:
  Host: matrix Kernel: 5.6.16-1-MANJARO x86_64 bits: 64 compiler: gcc
  v: 10.1.0 Desktop: i3 4.18.1 info: i3bar dm: LightDM 1.30.0
  Distro: Manjaro Linux
Machine:
  Type: Laptop System: Apple product: MacBookPro10,2 v: 1.0
  serial: <filter> Chassis: type: 10 v: Mac-AFD8A9D944EA4843
Battery:
  ID-1: BAT0 charge: 35.5 Wh condition: 65.9/73.9 Wh (89%)
  volts: 12.2/11.2 model: SMP bq20z451 type: Li-ion serial: N/A
  status: Charging cycles: 936
CPU:
  Topology: Dual Core model: Intel Core i5-3210M bits: 64 type: MT MCP
  arch: Ivy Bridge rev: 9 L2 cache: 3072 KiB
  flags: avx lm nx pae sse sse2 sse3 sse4_1 sse4_2 ssse3 vmx
  bogomips: 19961
  Speed: 1198 MHz min/max: 1200/3100 MHz Core speeds (MHz): 1: 1197
  2: 1196 3: 1198 4: 1197
Graphics:
  Device-1: Intel 3rd Gen Core processor Graphics vendor: Apple
  driver: i915 v: kernel bus ID: 00:02.0 chip ID: 8086:0166
  Display: x11 server: X.Org 1.20.8 driver: intel unloaded: modesetting
  alternate: fbdev,vesa compositor: compton resolution: 2560x1600~60Hz
  OpenGL: renderer: Mesa DRI Inte HD Graphics 4000 (IVB GT2)
  v: 4.2 Mesa 20.0.7 compat-v: 3.0 direct render: Yes
Audio:
  Device-1: Intel 7 Series/C216 Family High Definition Audio
  driver: snd_hda_intel v: kernel bus ID: 00:1b.0 chip ID: 8086:1e20
  Sound Server: ALSA v: k5.6.16-1-MANJARO
Network:
  Device-1: Broadcom and subsidiaries NetXtreme BCM57786 Gigabit
  Ethernet PCIe
  driver: N/A port: efa0 bus ID: 02:00.0 chip ID: 14e4:16a3
  Device-2: Broadcom and subsidiaries BCM4331 802.11a/b/g/n
  vendor: Apple AirPort Extreme driver: wl v: kernel port: efa0
  bus ID: 03:00.0 chip ID: 14e4:4331
  IF: wlp3s0 state: up mac: <filter>
Drives:
  Local Storage: total: 233.76 GiB used: 11.21 GiB (4.8%)
  ID-1: /dev/sda vendor: Apple model: SSD SM256E size: 233.76 GiB
  speed: 6.0 Gb/s serial: <filter> rev: 9A1Q scheme: GPT
Partition:
  ID-1: / size: 228.80 GiB used: 11.21 GiB (4.9%) fs: ext4
  dev: /dev/sda2
Sensors:
  System Temperatures: cpu: 52.0 C mobo: N/A
  Fan Speeds (RPM): N/A
```

During the configuration, I had some challenges. For example: resolution font size setup, screen flickering, terminal
powerline fonts setup, terminal switching and etc. So now I am going to talk about some of the fun stuff and hopefully
it can help other people who have the similar problems.

## Installation

The whole installation process was smooth. I downloaded an image from [Manajaro official website](https://manjaro.org/download/#i3),
and used [Etcher](https://www.balena.io/etcher/) to burn the USB installation drive since I was using a Mac.

When starting the machine, hold `option` key to enter the disk loading page, and use the USB to start. And then just follow
the steps.

As I mentioned above, I chose Manjaro Architect. The setup process was pretty straightforward most of the time, but there were
some tricky parts that I would like to discuss.

#### Partitioning

The partition was relatively easy regardless if you are dual booting or not. However, before partitioning your disk, make sure
you have enough space for your Linux partition.

Normally, you would have three partitions under the Linux partition: `/boot`, `/root`, and `/home`. That's pretty much enough. You also
can just have a boot partition and the other one for the rest of the use. But in my case, I created these three partitions. I put
1G to my `/boot` partition with the type of `FAT`, 30G to `/root`, and the rest to `/home`. Both `/root` and `/home` were using
`EXT4` as their partition type. If you are a tensive user, meaning that if you will install
a lot of programs, I would recommend you to increase your `/root` partition. But generally speaking, 30G is more than enough.
I didn't create the `swap` partition as it is nowadays not really needed. But feel free to create one if you need it.

#### DE and Packages

You could also select your favorite desktop environment during the installation process. e.g. KDE plasma, GNOME, XFCE, i3, and
etc. There are also tutorials on [YouTube](https://youtube.com) explaining the main process in detail. So I am not going to
discuss each of them, as it is really case by case. You would have to know what you need, though. But one good thing about
Manjaro Architect installation is it provides you the full and minimal installation. If you really are not sure where to start,
choose full installation. It will preinstall some packages and libraries by default. It also provides you the opportunity to
select which packages do you want preinstalled. Again, if you are not sure, just leave everything as default.

## Display Setup

### DPI and Fonts

I have a retina display laptop which has the resolution of 2560 x 1600. So right after I installed the system, the default font
size was too small for me. I needed to change the default display DPI for my new system. Here the .Xresource file was the one
that I should modify. This file controls the X client applications. It has the terminal
preferences setup, such as colors, DPIs, and other fun stuff.

I set my `Xft.dpi` as 120

```
Xft.dpi: 120
```

The fonts can be set up in here as well. For example, I installed `ZSH` as my shell environment with
[oh my zsh](https://github.com/ohmyzsh/ohmyzsh). If you have used `oh my zsh` before, then you must know that in order to
display some ascii symbols, you have to install Powerline. And then you will have to set font family and font size here,
for both system and terminal, here.

```
*.font: DejaVu Sans Mono for Powerline:pixelsize=16
```

Note that rxvt terminal is awesome, but the problem is that it doesn't support emojis very well. I ran in to this issue
where I wanted to display some emojis from my bash script. I tried several other solutions, the best one that I found is
`st`, `Simple Terminal` by [suckless](https://st.suckless.org/). There are a lot of repos on Github that help people to
configure it. Not only can it display unicode, emojis, and other stuff, but it is light and easy to install.

### Transparency and Style

We can set up the window transparency and other styles in `.Xresources` as well. In my case, for example, the transparency
of st and other windows can be set up as followed:

```
*.alpha:        1
st.alpha:       0.9

```

Where alpha is from 0 to 1, 0 being fully transparent.

Color change can be followed as what has already been in the `.Xresources` file. For example:

```
*background:                      #222D31
*foreground:                      #d8d8d8
*fading:                          8
*fadeColor:                       black
*cursorColor:                     #1ABB9B
*pointerColorBackground:          #2B2C2B
*pointerColorForeground:          #16A085
*color0:                          #222D31
*color8:                          #585858

```

I highly recommend `st` as it is light-weighted, simple to set up, and easy to use. And most importantly, it is suckless!

[Nerd Font](https://www.nerdfonts.com/) works pretty well for both `oh my zsh` and `vim-airline`, as well as symbols and
emojis, therefore the unicode icons work perfectly in `ranger`, which is also the default file manager on Manjaro i3.
Highly recommended!

## Broadcom Wireless Driver

### Screen Flickering

I have a Broadcom BCM57786 on this Mac. The first problem I noticed is that my screen flickered once the wifi was connected.
I found the issue while I was using the USB drive to install the OS. I wasn't thinking too much as I thought it was some
compatibility issue or something on the installer drive system. However, after the installation, the issue persisted. The
funny thing was once I disconnected from wifi, everything went back to normal, but with wifi connected, my screen was insanely
flickering. So logically, I thought it might be because of my graphic card driver. I searched almost everywhere and replaced
the driver multiple times, even reinstalled the system, but wasn't successful. And then I found a "trick", which was that if
I closed my laptop lid and reopened it, the issue was gone. It was pretty interesting as I couldn't figure out why that was
the case. I don't generally quite like the magic solution, but I decided to fix another problem(My wifi was super slow. It was
around 30kps which was unbelievable) and then come back. To my surprise, I got two birds with one stone.

### Wireless Card Driver Installation

As I said above, my Internet was incredibly slow on this machine while my other devices were normal. So I started to think that
my wireless card driver was not compatible, or there was some misconfiguration in my setup. In the next few hours, I had tried
different methods provided by different people, but none of them worked, until I found this
[thread](https://forum.manjaro.org/t/broadcom-wifi-driver-fails-to-install-properly/46316). The post answer explained the wireless
card drivers' problem really good, and broke down the solution crystal clear. I followed the instruction here and replaced the
drive, and it WORKED! The speed went from 30kps to 200ish mbps! Yay!

Moreover, it actually fixed the flickering screen problem! They all added up.

I believe this article benefits not only the Manjaro users, but all other distro users as well. People in Manjaro community are
helpful and responsive, which should be really appreciated.

## Apps

### Neomutt

I installed `Neomutt` as my mail terminal-based email application. The setup was easy. I used [mutt-wizard](https://github.com/LukeSmithxyz/mutt-wizard)
package created by [Luke](https://lukesmith.xyz/) and it worked great.

There were few things I did for customization. I installed `lynx` to view the html format in terminal, and `urlview` to
open the links on the browser from emails. Both applications are extremely light, and they work as expected. There are, of course,
some alternatives, and I think they are worth trying as well.

### Calcurse

`Calcurse` is another command line calender/reminder/to-do list terminal based application. It is light and fast. I installed it
from `pacman`. Nice and easy. I love it's simpleness and the lightning speed.

### Zathura

There are a lot of PDF readers in Linux. `Zathura` is terminal based minimal application. You can bind shortcut keys to it, but out
of the box, it supports vim movement.

### Polybar

`Polybar` can be a nice alternative for i3 default status bar. There are tons of different settings you can do with it. Check their
Github [repo](https://github.com/polybar/polybar) for the nice instruction. But basically, it provides a nice and easy, clean way
to write bash scripts to configure the status bar.

## Resources and References

1. My [dotfiles](https://github.com/jeddl/dotfiles). It will be constantly updating, as I will experiment different applications and
   environment. (I might do more research on [dwm](https://dwm.suckless.org/) and try it out.)

2. [Archwiki](https://wiki.archlinux.org/). It has EVERYTHING.

3. Luke Smith's dotfile [repo](https://github.com/LukeSmithxyz/voidrice), I used some of his scripts.

4. [Manjaro Forum](https://forum.manjaro.org/), where I found a bunch of useful posts and tips.

