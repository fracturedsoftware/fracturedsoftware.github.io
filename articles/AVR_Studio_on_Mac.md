--- 
layout: article 
title: Running AVR Studio on a Mac
---

I was inspired to write this post because I recently had to reinstall Windows and AVR Studio after upgrading to MacOs High Sierra and the process wasn’t completely straight forward, so I thought I’d do a write up for my own reference and maybe help a few others. All in all AVR Studio 4 works quite well - for a Windows program - once you get it set up.

So this post is about running AVR Studio 4 under Windows 10 using Virtualbox running under Mac OS High Sierra. I’ll explain why I chose Windows 10 and AVR Studio 4 below. This should also work for slightly older versions of the Mac OS.

### Installing Virtualbox

First you need to download Virtualbox and the Virtualbox Guest Additions. There is also an extension pack available but I have never needed or used this. The download for Virtualbox is easy to find on the [Virtualbox](http://www.virtualbox.org) website but the Guest Additions are a bit hidden away. Currently they can be found at [http://download.virtualbox.org/virtualbox](http://download.virtualbox.org/virtualbox). From here you have to navigate down the list to the latest stable release of Virtualbox (5.2.12 as of May 2018) and then look for VBoxGuestAdditions.iso within that directory.

After downloading these two files you can install Virtualbox, but not the guest additions, as they are installed once Windows 10 is up and running. When running Virtualbox for the first time I would definitely read the manual, particularly the first parts on how to instal Windows and set up the amount of memory to use etc. I would also set the memory and disk sizes to larger than the recommended minimum. You can apparently change these later but at least on an earlier version of Virtualbox I couldn’t and this is one of the reasons for completely reinstalling everything. I set my memory to 5GB (I have 12 GB of installed memory) and Hard Disk size to 50GB.

### Installing Windows 10 under Virtualbox

This turned out to be fairly straight forward. I chose Windows 10 because it can be downloaded from Microsofts website without a product key and it can be installed and used without activation. There are only a few restrictions which aren’t much of a problem. The actual details of loading Windows 10 can be easily found, for example [here](https://www.howtogeek.com/244678/you-dont-need-a-product-key-to-install-and-use-windows-10) so I won’t go into them in detail. Basically you need to download the Windows 10 .iso from [microsoft](https://www.microsoft.com/en-us/software-download/windows10ISO) then start up Virtualbox and load the Windows .iso. This is explained in the section 'Starting a new VM for the first time' in the Virtualbox manual.

Once you have Windows 10 up and running you need to instal the Virtualbox Guest Additions, which among other things allows you to create a shared folder or two on the Mac host, making it easy to transfer files - such as AVR Studio - from your Mac to Windows, rather than downloading them via the internet under Windows 10. Downloading via Windows 10 is quite doable under Virtualbox but I have never set this up. I always just download on the Mac side and transfer to Windows via a shared folder.

One note regarding shared folders is that they are accessed via the Network link on the sidebar of the Windows File Explorer. If after you have created them they are slow to load I found creating a mapped network drive (right click on the folder and select 'Map network drive') helps quite a bit.

### Installing AVR Studio

This is where things weren’t quite so straight forward - but it is possible to get things to run properly with some effort. It took bit of Googling but in the end everything worked.

The first thing to decide is which AVR Studio to use. If you Google around, for example [here](https://www.kanda.com/blog/microcontrollers/avr-microcontrollers/avrstudio-explored), you’ll soon find that Studio 7 runs slow under Virtualbox, and Studio 5 and 6 are not well liked. I have tried a few of these versions in the past and have always gone back to AVR Studio 4. Studio 7 to me always seemed like a step back with less functionality. So Studio 4 it is for me at least.

Next is which version of Studio 4. The last one available is Studio 4.19 but there seems to be a bug (see link above) where the AVR compiler toolset isn’t located properly. You can manually set this but I never got it to work. The general consensus is that you should use the previous version AVR Studio - 4.18. There is also a Service Pack 3 available for this version. All the versions of AVR Studio are available on the [Microchip website]( https://www.microchip.com/mplab/avr-support/avr-and-sam-downloads-archive) (they bought Atmel a while ago) so you can download them and transfer them across to Windows via your shared folder.

After you install AVR Studio and the Service Pack you would think that you are done but unfortunately not. If you try to create a project in Studio 4 and compile and run it you will discover that the compiler toolchain is missing. AVR Studio uses the GCC toolchain so you have to install this as well. I got the toolchain by Googling WinAVR which eventually led me to [this link](https://sourceforge.net/projects/winavr/files). Even though the toolchain looks old - the latest is from 2010 - it is still downloaded several thousand times a week so I downloaded the latest version and installed it. The toolchain is also available from Microchip from the same page where you downloaded AVR Studio 4 but I have no idea if they work or not with Studio 4.

After installing the WinAVR toolchain you are nearly done. However if you compile and run a simple program you will still get a lot of errors. At this point I nearly gave up and just installed Studio 7, which presumably works fine on the latest Windows, but as I said before it seems to miss a lot of the functionality of Studio 4. Fortunately after some research I came across [this post](http://smallshire.org.uk/sufficientlysmall/?p=689&preview=true) (UPDATE: link seems to be broken) which if you read then scroll down to comment #7 will lead you to [download this file](http://www.madwizard.org/download/electronics/msys-1.0-vista64.zip) which contains a modified .dll. The page explaining the root cause of the problem is at [madwizard](http://www.madwizard.org/electronics/articles/winavrvista). There is also an [AVR Freaks topic on the same problem](https://www.avrfreaks.net/forum/avr-gcc-dont-run-vista?name=PNphpBB2&file=viewtopic&t=44251), particularly from comment #32 onwards.

After downloading the dll you need to replace the existing msys-1.0.dll in the utils\bin subdirectory of your WinAVR directory. I just renamed the old dll to msys-1.0.dll.old1 as there was already an msys-1.0.dll.old in the directory! So it looks like that file has caused problems in the past!

So in short:

1. Download Virtualbox and the Virtualbox Guest Additions from Virtualbox.org
2. Install Virtualbox onto your Mac
3. Download and install Windows 10 within Virtualbox followed by the Virtualbox Guest Additions
4. Download and install AVRStudio 4.18 and its Service Pack from Microchip.com
5. Download and install WinAVR to get the GCC toolchain from Sourceforge
6. Replace a dll within the WinAVR utils\bin subdirectory with a modified dll available [here](http://www.madwizard.org/download/electronics/msys-1.0-vista64.zip)

After that everything should work! Hope this helps a few of you out there.

### UPDATE:
The author of the replacement dll has allowed me to host his dll. Please visit his site first but if you can't find it you can get a copy [here]({{ site.url }}/assets/downloads/msys-1.0.dll.zip ).
