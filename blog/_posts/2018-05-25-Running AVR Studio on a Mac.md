--- 
layout: article 
title: Running AVR Studio on a Mac
---

I recently had to reinstall Windows and AVR Studio after upgrading to MacOs High Sierra and the process wasn’t completely straight forward, so I thought I’d do a write up for my own reference and maybe help a few others. In the post I also explain why I chose AVR Studio 4 running on Windows 10, rather than a more recent version of AVR Studio. All in all AVR Studio 4 works quite well - for a Windows program - once you get it set up.

The [full post is here] but in short:

1. Download Virtualbox and the Virtualbox Guest Additions from Virtualbox.org
2. Install Virtualbox onto your Mac
3. Download and install Windows 10 within Virtualbox followed by the Virtualbox Guest
   Additions
4. Download and install AVRStudio 4.18 and its Service Pack from Microchip.com
5. Download and install WinAVR to get the GCC toolchain from Sourceforge
6. Replace a dll within the WinAVR utils\bin subdirectory with a modified dll available [here]

After that everything should work! Hope this helps a few of you out there.

**UPDATE:** The author of the replacement dll has allowed me to host his dll. Please visit his site first but if you can't find it you can get a copy [here][1].

[full post is here]: {{ site.fullurl }}/articles/AVR_Studio_on_Mac.html
[here]: http://www.madwizard.org/download/electronics/msys-1.0-vista64.zip
[1]: {{ site.url }}/assets/downloads/msys-1.0.dll.zip