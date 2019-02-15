--- 
layout: default 
title: Virtual Serial Port for OSX
---

While working on MacSim, my AVR simulator for OSX, I started thinking about how I might go about implementing a serial port peripheral so that the simulated AVR could communicate with the outside world. This turns out to be quite a difficult problem on OSX. However after quite a bit of trial and error I managed to get it at least partially working.

Unfortunately there are no working examples available that I can find to see what might be preventing it fully working. All old examples from Apple are way out of date and don't compile at all. I seem to have reached a point where it is a bit beyond me and have open sourced the project in the hope that someone might be able to figure out what is wrong. The project page is [here] and the source is hosted on [GitHub].

[here]: {{ site.url }}/articles/virtualserialport.html
[GitHub]: https://github.com/fracturedsoftware/Virtual-Serial-Port-for-OSX
