---
weight: 100
title: "Install with LUKS2"
description: "Alpine Linux on your device with GNOME, LUKS2 and BTRFS"
author: "Vladimir Blinkov"
icon: "menu_book"
date: "2025-03-28T23:31:35+03:00"
lastmod: "2025-03-28T23:31:35+03:00"
draft: false
toc: true
tags: ["Alpine Linux"]
---

## Preparing USB stick

Refer to [USB stick setup guide](setup-usb)

## Login

Input `root` and hit `Enter` to get started:

```bash {hl_lines=[6]}
...

Welcome to Alpine Linux 3.21
Kernel 6.12.13-0-lts on an x86_64 (/dev/tty1)

localhost login: root
```

## Keyboard Layout

{{< alert context="info" text="If your keyboard uses the standard QWERTY layout (common in the US), you can safely <strong>skip</strong> this section. " />}}

```bash {hl_lines=[1,8,17]}
~ $ setup-keymap

af    al    am    ara   at    az    ba    bd    be    bg    br    brai  by    ca    ch    cm    cn    cz    de    dk    dz    ee    
epo   es    fi    fo    fr    gb    ge    gh    gr    hr    hu    id    ie    il    in    iq    ir    is    it    jp    ke    kg    
kr    kz    la    latam lk    lt    lv    ma    md    me    mk    ml    mm    mt    my    ng    nl    no    nz    ph    pk    pl    
pt    ro    rs    ru    se    si    sk    sy    th    tj    tm    tr    tw    ua    us    uz    vn    

Select keyboard layout: [none] us

us-alt-intl            us-altgr-intl          us-chr                 us-colemak             us-colemak_dh          
us-colemak_dh_iso      us-colemak_dh_ortho    us-colemak_dh_wide     us-colemak_dh_wide_iso us-dvorak-alt-intl     
us-dvorak-classic      us-dvorak-intl         us-dvorak-l            us-dvorak-mac          us-dvorak-r            
us-dvorak              us-dvp                 us-euro                us-haw                 us-hbs                 
us-intl                us-mac                 us-norman              us-olpc2               us-rus                 
us-symbolic            us-workman-intl        us-workman             us                     

Select variant (or 'abort'): us
```

## Hostname

Your hostname is your computer's unique network name. Ensure it is distinct from other devices in your local network to avoid possible issues in the future.

```bash
~ $ setup-hostname nihon
```

{{< alert context="success" text="This sets the machine’s hostname to `nihon`." />}}

## Connect network

{{< tabs tabTotal="2">}}
{{% tab tabName="Wi-Fi" %}}

Just reproduce as shown:

```bash {hl_lines=[1,4]}
~ $ setup-interfaces -r
Available interfaces are: eth0 wlan0.
Enter '?' for help on bridges, bonding and vlans.
Which one do you want to initialize? (or '?' or 'done') [eth0] wlan0
```

Now it will show you available Wi-Fi spots.

```bash
Available wireless networks (scanning):
1) Rifu
2) Nihon
3) Guidelines
Type the wireless network name to connect to:
```

Now you can either enter the number of network or if it's not present here input anything (e.g. `r`) and hit `Enter` to scan again.

```bash {hl_lines=[1,9]}
Type the wireless network name to connect to: 2
Type the "Nihon" network Pre-Shared Key (will not echo): 
 * Caching service dependencies ...
 * /var/run/wpa_supplicant: creating directory
 * Starting WPA Supplicant ...
Ip address for wlan0? (or 'dhcp', 'none', '?') [dhcp]
Available interfaces are: eth0.
Enter '?' for help on bridges, bonding and vlans.
Which one do you want to initialize? (or '?' or 'done') [eth0] done
Do you want to do any manual network configuration? (y/n) [n]
```

{{% /tab %}}
{{% tab tabName="Wired" %}}

Just reproduce as shown:

```bash
~ $ setup-interfaces -r
Available interfaces are: eth0.
Enter '?' for help on bridges, bonding and vlans.
Which one do you want to initialize? (or '?' or 'done') [eth0] eth0
Ip address for eth0? (or 'dhcp', 'none', '?') [dhcp]
Do you want to do any manual network configuration? (y/n) [n]
```

{{% /tab %}}
{{< /tabs >}}

## Timezone

```bash {hl_lines=[1,15,30]}
~ $ setup-timezone

Africa/            Chile/             GB-Eire            Israel             Navajo             US/
America/           Cuba               GMT                Jamaica            PRC                UTC
Antarctica/        EET                GMT+0              Japan              PST8PDT            Universal
Arctic/            EST                GMT-0              Kwajalein          Pacific/           W-SU
Asia/              EST5EDT            GMT0               Libya              Poland             WET
Atlantic/          Egypt              Greenwich          MET                Portugal           Zulu
Australia/         Eire               HST                MST                ROC                leap-seconds.list
Brazil/            Etc/               Hongkong           MST7MDT            ROK                posixrules
CET                Europe/            Iceland            Mexico/            Singapore
CST6CDT            Factory            Indian/            NZ                 Turkey
Canada/            GB                 Iran               NZ-CHAT            UCT

Which timezone are you in? (or '?' or 'none') [UTC] Asia
Aden           Barnaul        Dili           Jayapura       Kuwait         Pontianak      Srednekolymsk  Urumqi
Almaty         Beirut         Dubai          Jerusalem      Macao          Pyongyang      Taipei         Ust-Nera
Amman          Bishkek        Dushanbe       Kabul          Macau          Qatar          Tashkent       Vientiane
Anadyr         Brunei         Famagusta      Kamchatka      Magadan        Qostanay       Tbilisi        Vladivostok
Aqtau          Calcutta       Gaza           Karachi        Makassar       Qyzylorda      Tehran         Yakutsk
Aqtobe         Chita          Harbin         Kashgar        Manila         Rangoon        Tel_Aviv       Yangon
Ashgabat       Choibalsan     Hebron         Kathmandu      Muscat         Riyadh         Thimbu         Yekaterinburg
Ashkhabad      Chongqing      Ho_Chi_Minh    Katmandu       Nicosia        Saigon         Thimphu        Yerevan
Atyrau         Chungking      Hong_Kong      Khandyga       Novokuznetsk   Sakhalin       Tokyo
Baghdad        Colombo        Hovd           Kolkata        Novosibirsk    Samarkand      Tomsk
Bahrain        Dacca          Irkutsk        Krasnoyarsk    Omsk           Seoul          Ujung_Pandang
Baku           Damascus       Istanbul       Kuala_Lumpur   Oral           Shanghai       Ulaanbaatar
Bangkok        Dhaka          Jakarta        Kuching        Phnom_Penh     Singapore      Ulan_Bator

What sub-timezone of 'Asia' are you in? (or '?') Kuwait
```

## Setup repositories

To find fastest mirror and enable community repo:

```bash
~ $ setup-apkrepos -f -c
```

{{< alert context="warning" text="This may take a while. (Typically 2-5 minutes)" />}}

If you want to edit manually, simply enter:

```bash
~ $ vi /etc/apk/repositories
```

For manual editing may also help [Official Alpine Linux mirror list](https://mirrors.alpinelinux.org/).

## Root password

Follow instructions after executing:

```bash
~ $ passwd
```

## NTP

We will use internal NTP for convenience:

```bash
~ $ setup-ntp busybox
```

{{< alert context="info" text="**NTP** (Network Time Protocol) service is what sets your clock to correct time and date using internet connection." />}}

## Partitioning

We need to install necessary packages for partitioning, filesystem, bootloader and so forth:

```bash
~ $ apk add lsblk gptfdisk cryptsetup lvm2 efibootmgr e2fsprogs btrfs-progs grub grub-efi
```

{{< tabs tabTotal="2">}}
{{% tab tabName="Wipe disk" %}}

{{< alert context="danger" text="These commands will **WIPE EVERYTHING** from your disk. If you have important data on your disk, switch the tab to **Leave disk data**." />}}

Check your disk path in `/dev`, in guide it would be `nvme0n1`, but you also could face `sda` or `vda`:

```bash
~ $ lsblk
```

Create new GPT table:
```bash {hl_lines=[1,12,19,21,27,37,45]}
~ $ gdisk /dev/nvme0n1
GPT fdisk (gdisk) version 1.0.9.1

Partition table scan:
  MBR: not present
  BSD: not present
  APM: not present
  GPT: not present

Creating new GPT entries in memory.

Command (? for help): o
This option deletes all partitions and creates a new protective MBR.
Proceed? (Y/N): Y

Command (? for help): n
Partition number (1-128, default 1): 
First sector (34-1000215182, default = 2048) or {+-}size{KMGTP}: 
Last sector (2048-1000215182, default = 1000214527) or {+-}size{KMGTP}: +512M
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300): ef00
Changed type of partition to 'EFI system partition'

Command (? for help): n
Partition number (2-128, default 2): 
First sector (34-1000215182, default = 1050624) or {+-}size{KMGTP}: 
Last sector (1050624-1000215182, default = 1000214527) or {+-}size{KMGTP}: +1G
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300):
Changed type of partition to 'Linux filesystem'

Command (? for help): n
Partition number (3-128, default 3): 
First sector (34-1000215182, default =  3147776) or {+-}size{KMGTP}: 
Last sector (3147776-1000215182, default = 1000214527) or {+-}size{KMGTP}:
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300): 8309
Changed type of partition to 'Linux LUKS'

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): Y
OK; writing new GUID partition table (GPT) to /dev/nvme0n1.
The operation has completed successfully.
```

{{% /tab %}}
{{% tab tabName="Leave disk data" %}}

{{< alert context="warning" text="Be careful to not wipe something important." />}}

Remember your disk path in `/dev`, in guide it would be `nvme0n1`, but you also could face `sda` or `vda`:

```bash
~ $ lsblk
```

Modify partitions in your disk. We need only these partitions:

{{< table >}}
| Partition | Filesystem type | Size |
|---------|--------|-----|
| EFI system partition | `ef00` | 512MB or 762MB |
| Linux filesystem | `8300` | 1GB |
| Linux LUKS | `8309` | 50GB+ |
{{< /table >}}

We can also use already existing, but not already fully filled EFI partition if there is any another 100MB of free space.

{{< alert context="danger" text="Do **NOT** create several EFI partitions on a single disk." />}}

To start modifying, enter:

```bash {hl_lines=[1,12]}
~ $ gdisk /dev/nvme0n1
GPT fdisk (gdisk) version 1.0.9.1

Partition table scan:
  MBR: not present
  BSD: not present
  APM: not present
  GPT: not present

Creating new GPT entries in memory.

Command (? for help): ?
```

{{< alert context="danger" text="Do **NOT** enter `o` command, it will wipe all data from your disk!" />}}

Here you need to modify partitions by yourself using help manual called by `?` command. After completing with that, continue.

{{% /tab %}}
{{< /tabs >}}

Load new partitions to `/dev`

```bash
~ $ partprobe /dev/nvme0n1
```

## Configuring LUKS2

Create new LUKS2 partition:

```bash
~ $ cryptsetup luksFormat -v -c aes-xts-plain64 -s 512 \
        --hash sha512 --pbkdf argon2id --iter-time 1000 \
        --use-random /dev/nvme0n1p3
```

Open it:

```bash
~ $ cryptsetup luksOpen /dev/nvme0n1p3 lvmcrypt
```

## Physical & Logical Volumes

A common recommendation is to allocate [SWAP](https://www.linux.com/news/all-about-linux-swap-space/) partition space equal to your RAM size (for working hibernation), but not lower than 8GB.

For root partition it is recommended to use at least 16GB on installation with GNOME Desktop. Enter value you sure be enough and leave other space for separated `/home`.

```bash
~ $ pvcreate /dev/mapper/lvmcrypt
    Physical volume "/dev/mapper/lvmcrypt" successfully created.

~ $ vgcreate vg /dev/mapper/lvmcrypt
    Volume group "vg" successfully created

~ $ lvcreate -L 32G vg -n swap
    Logical volume "swap" created.

~ $ lvcreate -L 100G vg -n root
    Logical volume "root" created.

~ $ lvcreate -l 100%FREE vg -n home
    Logical volume "home" created.
```

Small verification if everything is OK:

```bash
~ $ lvscan
      ACTIVE          '/dev/vg/swap' [32.00 GiB] inherit
      ACTIVE          '/dev/vg/root' [100.00 GiB] inherit
      ACTIVE          '/dev/vg/home' [355.92 GiB] inherit
```

## File Systems

Create VFAT file system for UEFI partition:

```bash
~ $ mkfs.vfat /dev/nvme0n1p1
```

Create EXT4 file system for `/boot`:

```bash
~ $ mkfs.ext4 /dev/nvme0n1p2
```

Create BTRFS file system for `/`:

```bash
~ $ mkfs.btrfs /dev/vg/root
```

Create BTRFS file system for `/home`:

```bash
~ $ mkfs.btrfs /dev/vg/home
```

Create SWAP:

```bash
~ $ mkswap /dev/vg/swap 
```

## Mount Points

Mount `root` partition to `/mnt` :

```bash
~ $ mount -t btrfs /dev/vg/root /mnt
```

Create `/mnt/home` dir:

```bash
~ $ mkdir /mnt/home
```

Mount `home` partition to `/mnt/home` :

```bash
~ $ mount -t btrfs /dev/vg/home /mnt/home
```

Create `/mnt/boot` dir:

```bash
~ $ mkdir /mnt/boot
```

Mount `/boot`:

```bash
~ $ mount -t ext4 /dev/nvme0n1p2 /mnt/boot
```

Create `/boot/efi` dir:

```bash
~ $ mkdir /mnt/boot/efi
```

Mount UEFI partition to `/mnt/boot/efi`:

```bash
~ $ mount -t vfat /dev/nvme0n1p1 /mnt/boot/efi
```

Check partition scheme:

```bash
~ $ lsblk
nvme0n1        259:0    0 476.9G  0 disk  
├─nvme0n1p1    259:1    0   511M  0 part  /mnt/boot/efi
├─nvme0n1p2    259:2    0     1G  0 part  /mnt/boot/
└─nvme0n1p3    259:3    0 476.4G  0 part  
  └─lvmcrypt   253:0    0 476.4G  0 crypt 
    ├─vg-swap 253:1    0    32G  0 lvm
    ├─vg-root 253:2    0   100G  0 lvm   /mnt
    └─vg-home 253:3    0 356.4G  0 lvm   /mnt/home
```

## Installing Alpine

As simple as

```bash
~ $ setup-disk -m sys /mnt
```

## GRUB settings

Let's mount and chroot to our fresh installation: 

```bash
~ $ mount -t proc /proc /mnt/proc
~ $ mount --rbind /dev /mnt/dev
~ $ mount --make-rslave /mnt/dev
~ $ mount --rbind /sys /mnt/sys
~ $ chroot /mnt
```

To open configuration file, enter

```bash
~ $ vi /etc/default/grub
```

and then hit `i` on the keyboard.

Add new `GRUB_PRELOAD_MODULES` line to config:

```bash {hl_lines=[2]}
...
GRUB_PRELOAD_MODULES="luks cryptodisk part_gpt lvm"
```

Add new cryptodisk parameter:

```bash {hl_lines=[3]}
...
GRUB_PRELOAD_MODULES="luks cryptodisk part_gpt lvm"
GRUB_ENABLE_CRYPTODISK=y
```

To save file, press `ESC` then write `:wq` and hit `Enter`.

## BTRFS

Tell Alpine to load module on startup:

```bash
~ $ echo btrfs >> /etc/modules
```

Now enable BTRFS scan service

```bash
~ $ rc-update add btrfs-scan boot
```

## SWAP

Open `fstab`

```bash
~ $ vi /etc/fstab
```

Add swap partition (highlighted line) into `fstab`

```bash {hl_lines=[3]}
/dev/vg/root	/	btrfs	rw,relatime,ssd,space_cache=v2,subvolid=5,subvol=/ 0 1
/dev/vg/home	/home	btrfs	rw,relatime,ssd,space_cache=v2,subvolid=5,subvol=/ 0 2
/dev/vg/swap    none    swap    defaults                                           0 0
...
```

Also enable swap service

```bash 
~ $ rc-update add swap boot
```

## GNOME

First, reboot to test changes

To exit chroot enter

```bash
~ $ exit
```

Then reboot

```bash
~ $ reboot
```

And then install & setup GNOME: refer to [GNOME setup guide](setup-gnome)