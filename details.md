# Overview

  This project is intended to have a mobile Kali Linux environment for testing and learning pentesting techniques. The idea is more geared towards Red Team style environment while another part of the project to be deveolped later is to learn more Blue Team techniques within a controlled environment. The name for the project comes from the fact that Kali linux's Avatar is a dragon. 

# Materials Used 

  For this project I am using a Lg Nexus 5x 32gig cellphone. Part of this reason is that the device is no longer supported due to a defect from the processor (see snapdragon 808 soldering issue:https://bgr.com/2018/02/01/lg-nexus-5x-bootloop-class-action-settlement/) and the Google Support on it ended already and should the preparation brick the device replacement parts are easier to come by and repair is less intensive. Other good reason is that Google Branded devices have the simplest form of Android to deal with and are basically meant as dev phones (at least the Nexus line was.) Also there is room for experimental expansion if deemed necessary. Due to the Chipset being similar to other related smartphones of that line there is a smaller market for expanded RAM/HDD space that can be easily added to the device. Parts would need to be sourced from a market like Alibaba and as of this post ususally retail around $80. This could potentially expand the device to a possible 4 gb of ram ( up from the 2 that this came with) and in rarer cases a possible 128 gb of space (max size sold was 32 originally.) This shouldn't be needed but would be a nice expansion and may possibly depending on the quality of the board would go around the SD808's soldering issue but would strongly suggest procuring a "donor" or "spare" phone to attempt this on in light of the risks involved. 

  There are other devices that are supported for this such as the original Google Pixel XL that would work better but I haven't tried this yet due to the fact that either nethunter was supported and Maru wasn't yet or the reverse was true. This was just the device I had on hand that had support from both projects. Your mileage may vary here. The only other device I had that would support both was an older Nexus 5, which could work as well but speed and battery life would be an issue. One other benefit for that though is that MaruOs's convergence feature works a bit better with the 5 as only a cable would be needed to connect it to a tv and it also supported wireless charging so if that was important it's and option and the device is cheap to come by these days. 
  
  The second thing we will need is a Testing environment to act as our "target". As this will eventually involve exploits it will be essential to make sure I am not treading the line of illegality. Luckiy there are a few spare computers and routers I have around that could make a test environment and there are plenty of online resourses to learn the theory and practice with. This would help however in learning scenarios in which compromising the device phyically ( ie: USB Rubber Ducky) would be necessary.

# Software 

  The main crux of this is what software would be used. As I have previoulsy next to no experience in this field I needed something flexible that I can replicate easily and follow back on. This would prove difficult for a Smartphone device. However with this being a mobile application in mind this is the limitation I will need to work around. 

The Nexus 5x will be using a Custom Android rom called MaruOs (https://maruos.com/) for it's operating system and we will be instaling Kali Linux Nethunter (https://www.kali.org/kali-linux-nethunter/) on top of it along with the Kali Linux Appstore on top of this (https://www.kali.org/news/kali-nethunter-app-store/). The reasoning is that while for most things Nethunter on it's own would be enough we needed to remove the need for Google and also the key feature of Maru is that it offers a "Desktop" mode using Debian Linux and can use a keyboard and mouse to give a full desktop environment as well. All that would be needed would be a compatible dock of somekind or an ability to stream to a larger screen. The limitation is that without the Google Apps Suite this limits to a phyical connection or MiraCast being used at present. The Kali Linux App Store gives an environment similar to F-droid (https://f-droid.org/en/) to get a suite of tools to be used. Also if using Fdroid Specifically the Kali Linux Store's repo can be added to Fdroid as well. 

 This also gives us the ability to add additional repos and apps to be used for some purposes. For example I added Bitwarden's repo in order for the rare password save and password creation. Yubikey's app for 2 factor authentication and password retention among others that I can add later.

  One of the other noted reasons I went with MaruOs for this is that their most recent build as of this project changed the base of the ROM. Instead of being based on AOSP (Android Open Source Project) exclusively it's now based around the LineageOs (previously CyanogenMod) ROMs instead. This gives the easier possibility of controling root acces for the lazy and that updates may come quicker (if at all in the devices case). This also means there is a better chance that some of the bug fixes to address the SD808's flaws would work better. For example there is a workaround to "turn off" the larger cores that cause the overheating issue that causes the solder to fail early. Also the ROM isn't too disimilar from Cyanogen's which is what Nethunter originally worked for so troubleshooting may be easier to work around.   Also in line is that the OS itself is lightweight. As Depending on the tools needed a full Chroot install can take up much needed valuable space. 


# Setup and Install 
  
Phone Prep: 

 - In order to set this up we'll need to make sure we have a few thing prepped and ready to go. As this would involve loading a Custom ROM and Recovery to the phone there is always the risk that the phone could be accidentally bricked. I realize much of this would be a leap of faith so I started with the basics of any Android Os development. There are many guides on this but the process is about the same. For the sake of simplicity I had downloaded the ADB ( android development bridge) tools previously and unlocked the phone with the now abandoned Android Root Toolkit ( https://www.wugfresh.com/nrt/, still works but no updates so it only covers Nexus devices). As I am currently using only Linux boxes if I were to do this again the process would be different. If you got this far this assumes you have some experience in the process. If not I would suggest following this guide to get the necessary tools on your operating system to start and follow them closely (https://wiki.lineageos.org/adb_fastboot_guide.html). After that we will need to make sure the phone is setup as well If you haven't followed the link all the way down and you should have) this will take you to the steps to enable the Dev options Typically it involves the following:
   - In the Phone's setting go to the the About Phone section 
   - look for the devices build number
   - tap that build number 10 times to unlock the developer settings ( this is the case with many Android phones)
   - go back to the settings menu
   - scroll down until you see the developer options
   - toggle the "OEM" unlocking option
   - scroll down and toggle the USB Debugging option as well. ( If the the phone is plugged in you will get a prompt to trust the device. Select yes)

With that setup you can go through the steps provided here: https://maruos.com/docs/devices/bullhead.html#install-maru-via-twrp to insall the custom recovery that will be needed. I'll outlay the steps here from the page.

  - Install Maru via TWRP
# Download
Download the latest update zip for your device (it will look like maru-v0.x.y-update-bullhead-<sha256>.zip)

(Optional) If you would like to restore access to the Play store, you can download a third-party Google Apps zip and install it alongside Maru during this installation process. ( I avoided this to save space and make sure Google doesn't have access to the device you really shouldn't need it unless you plan on casting to a Chromecast or something like that) 

Push the update zip to your device by opening up a terminal (Linux or Mac) or Command Prompt (Windows) and running the following:

$ adb push -p maru-v0.x.y-update-bullhead-xxxxxxxx.zip /sdcard/
TIP

You can also just download the update zip directly from your device's browser so you don't need to push it from your PC to your device.

# Backup
Reboot to TWRP custom recovery:
$ adb reboot recovery
You will now be in TWRP recovery.

Take a complete back-up before proceeding so it's easy to revert back if needed. Just tap Backup > Swipe to Backup.
# Install
When you are ready to install Maru, do the following:

Tap "Install"

Tap the Maru update zip you pushed earlier (you may need to scroll down)

Swipe right to confirm flash of Maru

Hit back till you are at the main screen, then Wipe

Swipe right to Factory Reset (this will still keep your back-ups on your sdcard)

Tap Reboot System

Note

You may be asked to install SuperSU to root your device. If you know what rooting your device means and want to have it rooted then go ahead. Otherwise, it's best to tap "Do Not Install". (If this doesn't you can grab the SU, or super user, file from Lineage's site just look for the version for 15.1 which was based on Android oreo 8.0)

Regardless of your installation method, the first boot will take a few minutes so please be patient.

However we will be making sure to not reboot the device just yet as detailed in the last step (and if you did that's fine just restart the device and reboot into recovery again by holding down the volume key when starting up the phone to access the bootloader/ recovery menu after enabling the developer options one more time..) 

Instead we're going to go ahead and install Nethunter. 

  - In order to do this on the computer go to https://www.offensive-security.com/kali-linux-nethunter-download/
  - Download the "NetNunter Nexus 5X Oreo" build of this ( As MaruOs is currently based on Android 8 this ensures less reasons to worry about something going wrong.) 
  - Next follow the instructions here: https://gitlab.com/kalilinux/nethunter/build-scripts/kali-nethunter-project/-/wikis/home. One side note about this. I have flashed this several times and the install screen tends to "hang" with the progress bar during the install sometimes. I have had to attempt to flash this a few times but a good indicator of if it's still installing is if the progress bar is still animated or when you touch it the phone still vibrates a bit. That said it can take a long while to install. Just be patient. 
  - Once Complete you can restart the phone
  - Once in the phone the next part we'll need to select the "Kali Linux Nethunter" App. It should be a dark grey icon with a dragon on it. There is a second one that will show later when we install the app store for it but this is the main nethunter application with some of the tools already in it and needs a bit more configuration.
  - Once the application is open select the menu icon in the upper left and then select Kali Chroot Manager
  - Once there install the Kali Chroot to get the full application suite of tools
  - Second issue I ran into constantly is that for whatever reason the Kali Linux CHMOD tends to not like to download when you're in the Kali Linux application. There is a way around that which is basically taking the CHMOD file from the download and saving it to the "/" file directory in the phone ( Basically when you connect your phone to your pc and open it just move the file the that location with all the other folders and not just the downloads or TWRP folder, CHMOD won't find it otherwise. The instructions on how to do this is here: 
    - Download The Nethunter Rom like Normal on your pc (or open the one you downloaded initially).
    - As this will be in a compressed file format Extract the file 
    - In the folder there will be a second zip file named something similar to "kalifs-full.tar.xz" this is the file you will need
    - Copy this zip file to the root folder of your Android device 
    - Then run the CHMOD install in the Nethunter application. 
    - You can choose the size of the install depending on available space on the device or what you actually need. 
  - Next we're going to install the Nethunter Application Store from here: https://gitlab.com/kalilinux/nethunter/apps/kali-nethunter-app/-/releases. You can either do this in the recovery or just copying the .apk file to the downloads and installing it from the phone itself. Either option is fine. 
  - While Normally this would be the stopping point I decided to add a few more things to the Kali Linux Store application. As this works like Fdroid you can still add additional repo in the settings. A list of known repos can be found here: https://forum.f-droid.org/t/known-repositories/721. I added repos for Bromite ( to replace Google Chrome. App is part of the GrapheneOs suite a completely privacy focused, hardened version of android and can be found here https://grapheneos.org/), Bitwarden as a password manager and password generator, The Guardian Project's repo ( Another privacy focused repo but some of the applications are outdate but this does give us access to TOR via Orbot and the Tor browser application. Here's their site if you wish to read more https://guardianproject.info/), Ember's Repo for the non-Google dependent version of Signal, a privacy focused messaging application. I also Installed MicroG as well to replace Google play services with their implementation although much of this can usually function without it. 
  - Going back into MaruOs itself there is another option we can add if we wish. Since it is based on LineageOs there are a few useful options within the developer settings we can use. First and most import is root access. As this phone is being made for pentesting and once again assuming this is why you would follow this then you should understand the risks that are being undertaken. Mind you much of this is to remain as unidenifiable in a test environment as possible but it's not perfect. I'm a novice so I may have my steps wrong here but one thing we need to be clear on is that root access is "Giving The keys to the Kingdom" for any applications needing it. That said any rouge application that has this access can brick your phone or if you left anything to identify you with find you easily or worse compromise your phone. So enable this option at your own risk and only if you know what you are doing. Another thing to add that may be redundant is that there is an option to enable a terminal within Android itself further down. This is basically giving a commandline interface to the Android shell and can come in handy as well. There are terminal Applications within the Kali suite of apps but its always a good thing to make note of this as well. Also once again make sure you have OEM unlocking and USB debugging access open again if they aren't already. This at least gives you  more of a chance to get back to recovery if you need to also once again with this being a Nexus 5x and dreaded SD808 solder issue you can still apply a patch to make the phone somewhat useable, abeit slower, by running the app to shut down the larger core and that requires access to recovery ( I'll list the link to this later.)  
  
With all this installed and running right I'm pretty much set with a full device to learn from. Next move will be developing a controled testing environment to practice on for both software and some physical tests to compromise a system. Mainly to start it will be port scanning for any holes and testing writing scripts for Man in the middle attacks and USB Rubber Ducky style attacks as well. Also will be using several old routers to work on learning to properly use Wifi cracking techniques. Much of this is basic but its a good foundation as sometimes the easiest things that work are the simple stuff that is often overlooked. 
