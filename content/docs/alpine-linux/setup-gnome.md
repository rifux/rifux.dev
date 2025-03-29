---
weight: 101
title: "Setup GNOME"
description: "Install and configure GNOME desktop environment for Alpine Linux."
icon: "article"
date: "2025-03-29T12:14:52+03:00"
lastmod: "2025-03-29T12:14:52+03:00"
draft: false
toc: true
---

## Installing GNOME

First, start desktop installer

```bash
~ $ setup-desktop
```

and enter your username, full name and setup password

```bash
Setup a user? (enter a lower-case loginname, or 'no') [no] rifu
Full name for user rifu [rifu] Rifu Nihon
```

Input `gnome` desktop environment when prompted

```bash
Which desktop environment? ('gnome', ... or 'none') [none] gnome
```

## Setup user

Add yourself to `plugdev` to manage connections without root access and `wheel` to gain root access using `doas`

```bash
usermod -aG plugdev rifu
usermod -aG wheel rifu
```

Install `doas` itself

```bash
apk add doas
```

Now it's time to configure doas. To open configuration file, enter:

```bash
vi /etc/doas.conf
```

and then hit `i` on the keyboard.

Uncomment the line with `:wheel` here 

```bash {hl_lines=[5]}
# See doas.conf(5) and doas.d(5) for configuration details.
# Configuration here may be overridden by /etc/doas.d/*.conf if files exist.

# Uncomment to allow group "wheel" to become root.
permit persist :wheel
```

To save file, press `ESC` then write `:wq` and hit `Enter`.

## Setup NetworkManager

Install necessary packages for Bluetooth and Wi-Fi

```bash
apk add networkmanager-wifi networkmanager-bluetooth networkmanager-dnsmasq bluez
```

Enable Bluetooth

```bash
rc-update add bluetooth default
```

Enable NetworkManager

```bash
rc-update add networkmanager
```

Configure 

```bash
vi /etc/NetworkManager/NetworkManager.conf
```

reproduce these settings

```bash
[main] 
dhcp=internal
plugins=ifupdown,keyfile

[ifupdown]
managed=true

[device]
wifi.scan-rand-mac-address=yes
wifi.backend=wpa_supplicant
```

## More locales support

Add ICU & musl with non-English locales too

```bash
apk add icu-data-full musl-locales
```

## Add firmware & drivers

To have better software compatibility, you should install:

```bash
apk add linux-firmware mesa-va-gallium
```

If you have Intel GPU (since Intel Broadwell) also install

```bash
apk add intel-media-driver
```

## Remember brightness

Every boot you may notice that the brightness isn't saving after changing it on your device in GNOME quick setting panel, so here is the fix.

First, install `brightnessctl`:

```bash
apk add brightnessctl
```

Second, make it working from boot

```bash
rc-update add brightnessctl boot
```

and now you can notice brightness change back to normal while booting.

## Power profiles

Showcase

![](https://i.ibb.co/8g986Rj1/power-profiles-daemon.png)

Installation

```bash
apk add power-profiles-daemon
```

## GNOME Software

For apk package management through the GNOME Software, run

```bash
rc-update add apk-polkit-server
```

## Fonts support

For Japanese support

```bash
apk add font-terminus font-noto font-noto-thai font-noto-tibetan font-ipa font-sony-misc font-jis-misc
```

For other please refer to [Alpine Wiki](https://wiki.alpinelinux.org/wiki/Fonts#Installation)

## Boot into GNOME

Finishing our setup. So let's take a bite of it.

Reboot the system and see the result:

```bash
reboot
```