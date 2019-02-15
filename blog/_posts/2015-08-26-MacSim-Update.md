---
layout: default
title: New Update for MacSim
---

I am pleased to announce a new update to MacSim. It's been a long time coming and it nearly didn't happen, so I thought I'd explain what went wrong.

While working on the previous version of MacSim I thought I’d take some time out to implement one of the peripherals - a timer - to see how it went and if I could integrate it into MacSim without too many changes. Things went pretty well for a while, but at some point before I’d got more than a few of the different timer modes ‘working’ it all started going south. Every time I modified one part of the timer in order to get it to work, other parts would start behaving incorrectly.

I spent nearly 3 weeks running test programs on my simulator and comparing the results with AVR Studio. The results would often be identical for a while but then would begin to differ slightly, so I’d make a small change to the timer code to fix it but that would then cause other problems.At some point I more or less gave up, thinking that a microcontroller simulator without any peripherals wouldn't be that useful and I didn’t feel like spending ages futzing about trying to make it work. So the project languished until…

A few months ago while updating some projects that use a common framework I have been working on, I took another look at MacSim to see if it was worth updating to use the new framework. I’d really enjoyed working on it at the time ( apart from the last couple of weeks ) and it seemed a bit of a shame just to let it die. I was actually pretty close to getting the core working really well when I’d abandoned it and it would surely be moderately useful even without any peripherals. A few weeks work would get it up to date and hopefully I could then gradually add a few improvements that I had planned all along.

I even started thinking that I’d probably been a bit too hard with the timer testing. I had written some rather pathological code - changing timer modes just as the timer hit top or bottom and things like that, so maybe if I stuck to more realistic testing things work work out better!

So that is basically it. The simulator has been extensively updated and is working well and I am looking forward to implementing some improvements. There may be some incorrect instructions, so if you see any please let me know as they shouldn't be too hard to fix.