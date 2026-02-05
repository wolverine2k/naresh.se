---
title: "OpenWRT Client Mode"
date: 2026-02-05
categories: 
  - "general"
  - "OpenWrt"
tags: 
  - "OpenWrt"
  - "Client Mode"
  - "AC-1204" 
  - "GJ2CQ"
---

I got a bunch of Gale (Google Wifi devices) on an auction site as broken. The owner of the devices was basically saying that all the devices were working but randomly shutting down. To make them work again, they had to be unplugged and replugged. So he/she auctioned them off as replacement devices at an ultra low price (3 AC-1204 and 2 GJ2CQ models) of 30$ for all 5. I of course had to get it. Power doesn't seem to be an issue. Mostly a SW conflict due to the configuration being used by the previous owner.

The first thing that I had to do was load OpenWRT on the AC-1204. Read my article on [OpenWrt on Google Wifi](https://naresh.se/en/posts/202425/2025-04-29_openwrt-on-google-wifi/) for more details. Once the devices had OpenWRT running, the next thing was to make sure that they are updated and I resize the partitions to use all the available space. There were 2 options for me:
1. Plugin the device on my main network physically and then use the LAN interface to get the updates
2. Use the new router as a client in my existing network and route the VLAN traffic to it

Option 1 is disruptive as it would bring down the network in the whole house. Option 2 is easier (said then done). But there are a couple of roadblocks to configure the router in client mode and route the VLAN traffic through it. This is my learnings and notes for the future (and anyone) who does not play with the router all the time.

## Client Mode Configuration

Below are the steps to get the client mode to work:
1. Login to LUCI. The default OpenWRT interface is 192.168.1.1. Since it is a fresh flash, the root password is empty. So login with root and empty password.
2. Go to Network -> Interfaces, select the br-lan interface and click on Edit.
3. Change the Protocol to Static and set the IP address to 192.168.11.1 (Make it different from the default main router if it also exhibits 192.168.1.1).
4. Reboot and login to the new IP
5. Go to Network -> Interfaces again, select the br-lan interface and click on Edit.
7. Set the Gateway IP address to 192.168.1.1 (If you main-router is using 192.168.1.1).
8. Goto Network -> Wireless and remove the default 2 SSID configuration.
9. Click on the Radio0 (ac/N or b/g/n) and select Scan.
10. Connect to your Wifi network.
11. Now go to Firewall -> General Settings Zones. 
12. Default firewall settings reject forwards from wan.
13. Edit the configuration to accept forwards from wan to lan including input, output and intra zone forwards.

Reboot the router and enjoy. Now your router has full connectivity from the wireless to the wired network. Between, always connect to the router you are setting up via cable so it is easy to recover in case of errors. Now try opkg update and opkg upgrade to update the packages. If the update fails with no path to downloads.openwrt.*, use a browser to openwrt [downloads url](https://downloads.openwrt.org/releases/25.02.0/packages/aarch64_cortex-a53/packages/). That should flush the dns cache.

Now you have a router that can route the VLAN traffic to the main router. You can use it as a client in your existing network. Once the configuration is done, setup your password on root, back-up the configuration and you are good to go.

Next step is to setup the mesh network (802.11s). I will write a separate article on that.
