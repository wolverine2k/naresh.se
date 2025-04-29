---
title: "OpenWrt on Google Wifi"
date: 2025-04-29
categories: 
  - "general"
  - "technology"
tags: 
  - "openwrt"
  - "google"
  - "wifi"
  - "router"
---

[OpenWrt](https://openwrt.org/) is a great router firmware with lots of features, flexibility and security updates. It is basically a small Linux distribution and does a smart job at adding enhancements to any "supported" router. One can read more about it [here](https://openwrt.org/reasons_to_use_openwrt).

I have been using [Google Wifi](https://www.google.com/wifi) for a while now and it has been a great experience. It has an amazing HW (4GB of storage and 512MB of RAM). Google SW can be controlled using Google Home but privacy, DNS, parental controls, firewall, ad-blocking and other features are either not supported or are not as good as I would like them to be. And also my version of the Wifi AC-1304 does not receive any new features.

Some years ago, I had experimented with [Galeforce](https://github.com/marcosscriven/galeforce) but the project has been dead for almost 8+ years. I [forked](https://github.com/wolverine2k/galeforce) and added some features, and played around with it. But I couldn't get it to stick as the Google SW would always revert back to the default SW and disable my SSH access.

I kind of gave up on it. But a couple of months ago, I by chance came to know that [OpenWrt now supports Google Wifi](https://openwrt.org/toh/google/wifi)! All the instructions and step-by-step guide is available on that webpage. The best part is that I can now use the full 4GB of eMMC storage. With the 512 MB RAM available, OpenWrt creates one of the most powerful home routers available. Once the router is loaded with OpenWrt, it does not work with Google Home anymore but who cares? I have a super powerful device at my disposal.

On my OpenWrt setup, I have adblocking, DNS filtering, parental controls, firewall, VPN, QoS, etc. enabled. I also have a custom script that runs on boot to set up my router. I am also going to host zeroTier so that I can access my self-hosted NAS from outside world (WIP). The router is very stable and I do not see any performance or functional issues. In fact, I have not seen any issues at all. On my network, I have a LAN only router running OpenWrt which then is connected to the Google Wifi router. With this setup, I have 2 layers of protection. All my devices are on the Google Wifi OpenWrt.

My OpenWrt Google Wifi is barely using any resources at all. It is using about 250MB or RAM and 35MB of the 4GB storage available. So I am pretty sure I can setup more services including DDNS, Zerotier and/or cloudfare tunnels.

I will keep you all updated. Nothing can beat OpenWrt!
