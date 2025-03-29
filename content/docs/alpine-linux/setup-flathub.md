---
weight: 210
title: "Setup Flathub"
description: "Install Flatpak & GUI"
author: "Vladimir Blinkov"
icon: "menu_book"
date: "2025-03-29T11:48:57+03:00"
lastmod: "2025-03-29T11:48:57+03:00"
draft: false
toc: true
tags: ["Alpine Linux"]
---

## Install Flatpak

Community repository needs to be working. If so, run in terminal:

```bash
doas apk add flatpak
```

## Install the GUI Flatpak plugin

You can install the Flatpak plugin for either the GNOME Software (since v3.13) or KDE Discover (since v3.11), making it possible to install apps without needing the command line.

{{< tabs tabTotal="2">}}
{{% tab tabName="GNOME Software" %}}

```bash
doas apk add gnome-software-plugin-flatpak
```

{{% /tab %}}
{{% tab tabName="KDE Discover" %}}

```bash
doas apk add discover-backend-flatpak
```

{{% /tab %}}
{{< /tabs >}}

{{< alert context="info" text="It may require restarting the system or re-login to load plugins" />}}

## Add Flathub repo itself

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Restart system

Now it's recommended to reload all the stuff to surely make it working

```bash
doas reboot
```