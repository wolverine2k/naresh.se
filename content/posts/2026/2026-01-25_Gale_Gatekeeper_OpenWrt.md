---
title: "Gatekeeper for OpenWrt - Control devices on your Wifi"
date: 2026-01-25
categories: 
  - "general"
  - "Security"
  - "OpenWrt"
tags: 
  - "Gatekeeper"
  - "OpenWrt"
  - "Security"
  - "Gale"
---

[Gale-Gatekeeper](https://github.com/wolverine2k/gale-gatekeeper/) is a security tool that allows you to control devices on your Wifi. [Gale-Gatekeeper](https://github.com/wolverine2k/gale-gatekeeper/) is a Telegram-based network access control system for OpenWrt routers. When a new device connects to the network via DHCP, the system sends a Telegram notification with interactive Approve/Deny buttons. Devices with static DHCP leases are automatically allowed. Temporary devices require manual approval and have timeout-based access (30 minutes default).

I was so tired of the impossibility to control the wifi devices on my network. My kids used to jump devices from one to another. I also got a host of devices from school which I had no control over. So my kids basically got access to the internet almost 24x7 jumping devices. I have been trying very hard to implement a effort-reward mechanism but it was not working as I had no/almost 0 control over the screen time for my kids.

My whole house is also connected with a host of various appliances so I had to make sure that those devices are never interrupted or have broken internet connections. Firewalling devices is a hazzle and I also have to log into the router (ssh or LuCi) to do it. Again, because of the huge number of devices, I would like to have my normal "connected" devices just rush through the firewall but allow me control to have other/unknown devices to be approved/denied by me. And the approvals/denials should automatically be reset after a certain period of time.

So I decided to write the [Gale-Gatekeeper](https://github.com/wolverine2k/gale-gatekeeper/). As you might have realized, I am running openWRT on my Google Wifi Router (Gale). Read the details on [OpenWrt on Google Wifi](https://naresh.se/en/posts/202425/2025-04-29_openwrt-on-google-wifi/). The best part with OpenWRT is the flexibility and controllability that comes with it. I scoured the internet for a solution but could not find one that was simple to use and easy to configure. And hence was born Gale-Gatekeeper.

It is a set of scripts which does the following:
1. Monitors the DHCP requests and sends a Telegram notification with interactive Approve/Deny buttons.
2. Devices with static DHCP leases are automatically allowed.
3. Temporary devices require manual approval and have timeout-based access (30 minutes default).

Yes, as simple as that. And it works flawlessly. Details are available in [CLAUDE.md](https://github.com/wolverine2k/gale-gatekeeper/blob/main/CLAUDE.md). Yes, I have got help from Claude to write the archtecture & documentation details and some cursor help to make it more configurable. I have also added extra commands like "status", "sync", "log", "disable", etc. to make it more user-friendly. Below is a picture of the Telegram notifications.

![Telegram Notification](https://live.staticflickr.com/65535/55059822661_b7df8d4c9a_c.jpg)

The emergency "disable" button disables the gate-keeping functionality. This is useful when you want to allow all devices to connect to the network without any approval or if the gatekeeper is not behaving properly. The "sync" command syncs the gatekeeper with the current DHCP leases. The "status" command shows the current status of the gatekeeper. The "log" command shows the logs of the gatekeeper. The "enable" command enables the gatekeeper.

The best part is once you disapprove a device, it will not be allowed to connect to the network and all notifications regarding the device asking for connection will stop for 30 minutes. Similarly the approval is valid for 30 minutes as well. The approval request from a device comes automatically. i.e. a user of the device does not need to do anything special to send a notification. If you as a user do not approve/deny the request, it will be denied automatically after 5 minutes. And no new notification for that device pops up for 30 minutes.

Gale-Gatekeeper gives you ultimate control on the devices connected to your network. Now just knowing your Wifi password isn't enough. You as a parent/owner of the network can control which devices are allowed to connect to the network and which devices will have its packets dropped by the firewall. Except for the statically configured leases, everything else is controlled by you. A device which is spoofing or changing MACs to bypass static firewall rules is a thing of the past.

Use the [Gale-Gatekeeper](https://github.com/wolverine2k/gale-gatekeeper/) on your #OpenWRT router. All comments/enhancements/bug reports are welcome. Please open an issue on the [GitHub repository](https://github.com/wolverine2k/gale-gatekeeper/). Looking forward to your feedback and suggestions.