---
layout: article
title: Virtual Serial Port for OSX
description: Software to emulate a physical serial port on Mac OSX. A work in progress.
---

While working on MacSim, my AVR simulator for OSX, I started thinking about how I might go about implementing a serial port peripheral so that the simulated AVR could communicate with the outside world. This turns out to be quite a difficult problem on OSX.
	
Since no Mac actually has a serial port, the port is handled via USB and a serial driver in the form of a kernel extension has to be implemented to provide a communication channel between the serial device and the operating system. When you plug in a USB serial device, such as an Arduino, the OS detects this and loads an appropriate serial driver. In the case of virtual hardware, such as MacSim, the application has to load this kernel extension at the appropriate time and do the communication, which is at a very low level. Debugging all this is difficult as everything takes place deep within the kernel and normal application debugging can't be used.

Just to add to the difficulty, although the Mac serial ports are implemented much like on other unix systems at a lower level, virtually all Mac serial software gain access the serial ports at a much higher level, via I/O Kit, so this has to be implemented as well.
	
Finally, this is a fairly specialised area - one that I am totally unfamiliar with - so there are virtually no fully working serial driver examples and help is hard to find.

Despite all this I have managed to get a partially working example, which I have open sourced. Part of the reason for open sourcing it is because I am hoping someone with a bit more knowledge may be able to help to get it going properly. At the moment you can only send messages one way, from your virtual hardware to a terminal program, but not the reverse. 

### There are a few very important caveats if you want to experiment with this:

1. Because this project creates a kernel extension - kext - if anything goes wrong the usual result is that it MAY crash your computer, rather than     just quitting like a normal app, unless you are a bit careful. Maybe even then. It hasn't crashed for me for a while though.
2. Also, to use the kext, since it is unsigned you will have to remove the 'System Integrity Protection' on your computer before it can be loaded. This sounds ominous so you need to do your own research. Of course if you have an Apple Developer account you could sign the kext as part of the build process so you won't have to do this. If I manage to get this working properly and use it within MacSim the kext will be available signed. 
3. The kext has to be loaded manually, though this isn't difficult and instructions to do so are included. The download has more details. A real app with a signed kext would be able to load the kext automatically.

The complete source with instructions is available on [GitHub](https://github.com/fracturedsoftware/Virtual-Serial-Port-for-OSX).
