---
title: "Magisk Out, APatch IN!"
date: 2025-05-05
categories: 
  - "general"
  - "technology"
tags: 
  - "Magisk"
  - "Apatch"
  - "android"
  - "root"
---

I have been using [Magisk](https://topjohnwu.github.io/Magisk/) since almost 12 years now when I first started rooting and unlocking my bootloaders and using/creating my custom ROMs. Magisk allowed for managing root access to applications, install modules that allowed for functionality that is not available otherwise, access the android application's process space using Zygisk, lsposed and associated modules, etc. Without Magisk, if one had unlocked bootloader and rooted his/her device, it would be a nightmare to manage root access and host load of applications will start failing because of the "compromised security".

Magisk has been a long and faithful companion for any Android user who has unlocked bootloader and rooted his/her device. Magisk though had only one weakness and that was that it ran in user space. Many applications would scan the installed list of applications and would curtail functionality or even refuse to run if they detected Magisk installed. Magisk found a way to install itself using randomized names & icons but still, these solutions were patches and not a permanent fix. Someone found a way to detect it and then a patch was created to defeat that detection. Also, moving from one Android version to another poses its own problems.

Branching into Magisk, Magisk Canary and Magisk Beta brought in its own peculiar tweaks and each version was incompatible, broke modules and/or with stability issues. If I wanted to replicate a similar behavior from one device to another, it was a nightmare and the gaurantees of it working were minimal. Every new device, based on the Android version will always have newer issues with applications. 

Don't get me wrong here. I still love Magisk and I will continue to use it for my custom ROMs and for my devices but it is becoming a bit cumbersome. [Kernel SU](https://github.com/tiann/KernelSU) is a much better option as the root management is from kernel space but it requires the kernel source and kernel recompilation. So if one has just unlocked the bootloader and rooted his/her device, he/she will need to recompile the kernel with the KSU patch and install it. Just additional manual hassle. Also, latest KSU does not work with non-GKI kernels (v1.0 and later versions). The last supported version for [non-GKI kernel is v0.9.5](https://kernelsu.org/guide/how-to-integrate-for-non-gki.html) and is a bit of a hazzle to install.

With [APatch](https://apatch.dev/), we have a much better option. Apatch runs in kernel space and makes the detection much more difficult as the APatch is running in Kernel Space. The root priviledges are directly granted in kernel space. The best part is that APatch does not need the kernel source or kernel recompilation. APatch is kernel-based root-access control with APModule (Magisk like module support) and KPModule (Kernel inline-hooks). The easy way is to just install the [APatch APK](https://github.com/bmax121/APatch?ref=akpatch.org). Latest release is 11039 and can be fetched from [github](https://github.com/bmax121/APatch/releases/tag/11039).

The process to install APatch is very simple. The steps are as below:

1. Extract boot.img from the device. Doing this with custom recovery is the easiest way. I used TWRP for this.
```
adb shell
dd if=/dev/block/bootdevice/by-name/boot of=/sdcard/boot.img
exit
adb pull /sdcard/boot.img
```

The above will extract the running boot.img. Between, if someone is skirmish about installing custom recovery, just boot into the custom recovery using fastboot and let the original recovery be as it is. You can boot into the custom recovery using the following command:
```
fastboot boot <path_to_custom_recovery.img>
```

2. Open the APatch apk that was installed on the device.
3. Open the boot.img file that was extracted in step 1 and patch it.
4. This should generate a APatch_Patched_boot.img in the /sdcard/Download/ folder.
5. Get the image on your PC using the following command:
```
adb pull /sdcard/Download/APatch_Patched_boot.img
```
6. Flash the boot.img using fastboot:
```
fastboot flash boot APatch_Patched_boot.img
```
7. Reboot the device:
```
fastboot reboot
```

Voila, APatch is installed and running. You can now use the APatch apk to install modules and manage root access. Some of the basic modules that I recommend are:

- [PlayIntegrityFix](https://github.com/chiteroman/PlayIntegrityFix)
- [Zygisk Next](https://github.com/Dr-TSNG/ZygiskNext) or [Zygisk Mod](https://github.com/Admirepowered/Zygisk_mod)
- [Zygisk Assistant](https://github.com/snake-4/Zygisk-Assistant)
- [LSposed Fork](https://github.com/JingMatrix/LSPosed)
- [Tricky Store](https://github.com/5ec1cff/TrickyStore)

And ofcourse the usual [Pixelify](https://github.com/Kingsman44/Pixelify) and [Hide My Applist](https://github.com/Dr-TSNG/Hide-My-Applist).

More details available on [XDA](https://xdaforums.com/t/dev-apatch-an-alternative-root-solution-to-kernelsu-and-magisk.4655727/).

Enjoy the new experience!