---
layout: post
title: "Installing PixHack v5 on Heli"
---
![pixhack]({{site.baseurl}}/images/phinstall/pixhackv5.png)

Today the PixHack v5 arrived and I didn't hesitate to start installing the hardware on the Blade 360 CFX. I knew it was going to be cramped to get everything on but it all seemed to fit. 

The install approach I took was somewhat unconventional in that I didn't remove the pre-existing flybarless (FBL) control unit. My reasoning was to enable flight testing with the new hardware installed in order to ensure the flight characteristics are still acceptable. This is rather important as I have no experience utilizing ArduPilot and will be using a new [Taranis Q X7S](https://www.frsky-rc.com/product/taranis-q-x7s/) radio... so adjusting the control gains to mimic the flight characteristics I am used to will be interesting, especially since I'm not a great heli pilot.

The base is comprised of some balsa wood spacing and thing modeling plywood that is glued together. This assembly is then attached to the bottom of the helicopter with two screws which threaded directly into the carbon fiber frame.

![basebtm]({{site.baseurl}}/images/phinstall/basebottomview.png){:width="90%"}
![baseside]({{site.baseurl}}/images/phinstall/basesideview.png){:width="90%"}

The PixHack flight controller is then attached using Velcro. Additional Velcro straps are used to ensure it can't fall off during flight.

![velcro]({{site.baseurl}}/images/phinstall/velcroattachment.png){:width="90%"}
![velcrostrap]({{site.baseurl}}/images/phinstall/velcrostraps.png)

The GPS was attached to the tail boom using super sticky (the black kind) double stick tape along with some clamps that provided more surface area for adhesion.

![gps]({{site.baseurl}}/images/phinstall/gps.png){:width="90%"}
![gpsSticky]({{site.baseurl}}/images/phinstall/gpssticky.png)

Re-routing the power cable from the speed controller with the addition of the power supply was a bit finicky. This would of been easier had I consolidated the power connection types but I figured I would be lazy and use adapters to go between the XT-60 connections on the PixHack power supply and the existing EC3 connectors. To facilitate flight testing I affixed the new [X8R](https://www.frsky-rc.com/product/x8r/) receiver on top of the original FBL control unit. 

![overview1]({{site.baseurl}}/images/phinstall/overview1.png)
![overview2]({{site.baseurl}}/images/phinstall/overview2.png) 

## What's Next
* flight test with the new hardware using the original control setup
* bind the Q X7S radio to the X8R receiver
* ensure the Q X7S is properly configured for basic heli flight
* connect the PixHack v5 to [QGroundControl](http://qgroundcontrol.com/) to ensure its properly configured
* configure the PixHack v5 for my installation orientation and heli setup
* flight test with factory installed firmware on the PixHack v5?
* install ArduPilot Copter 3.6 firmware on the PixHack v5
* flight test with Copter 3.6