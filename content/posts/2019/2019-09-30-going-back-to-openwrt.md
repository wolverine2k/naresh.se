---
title: "Going back to OpenWRT"
date: 2019-09-30
categories: 
  - "general"
  - "ib467n-strategy-benefits-and-alignment"
  - "studies"
  - "technical"
tags: 
  - "gargoyle"
  - "netgear"
  - "openwrt"
  - "r6220"
---

About a couple of months ago, I went from OpenWRT to Gargoyle on my Netgear R6220 router. You can read more about it [here](https://www.naresh.se/2019/07/01/compile-gargoyle-for-netgear-r6220/). I had setup a couple of networks with one hidden and not isolating clients whereas the other one doing the reverse. Now everything was OK but the Gargoyle used to crash my kernel whenever a new device tried to join the unadvertised network. The different interfaces were also brought down. Again, there are certain features of OpenWRT that I really missed with one being the ability to create multiple virtual radio interfaces and the other being the flexibility with adblock host lists.

So, I wanted to go back to OpenWRT. Gargoyle runs on top of OpenWRT but both the kernel and the rootfs were modified to a very big extent by Gargoyle. Telent was not enabled and doing a sysupgrade didn't work for me. So I did the following procedure to get back to OpenWRT from Gargoyle.

```
root@Andromeda:~# cat /proc/mtd
dev:    size   erasesize  name
mtd0: 00100000 00020000 "u-boot"
mtd1: 00100000 00020000 "SC PID"
mtd2: 00400000 00020000 "kernel"
mtd3: 01c00000 00020000 "ubi"
mtd4: 00100000 00020000 "factory"
mtd5: 03c00000 00020000 "reserved"
```

As can be seen above there are 6 mtd devices on the R6220. MTD2 (kernel) and MTD3 (ubi) are the kernel and the rootfs respectively. Since sysupgrade was throwing invalid file format errors, I had to do mtd writes on the respective MTD devices directly using the command below.

```
mtd -r write /tmp/kernel.bin kernel
mtd -r write /tmp/rootfs.bin ubi
```

The above allowed me to go back to OpenWRT without the LUCI interface.

```
opkg update
opkg install luci
```

Allowed me to install Luci and configure my router like normal. In the middle, I did need to do a

```
sysupgrade -n -v /tmp/sysupgrade.bin
```

to get to a nice working OpenWRT version. The packages for the router are available on ["OpenWRT Snapshots"](https://downloads.openwrt.org/snapshots/targets/ramips/mt7621/). Hope this helps!
