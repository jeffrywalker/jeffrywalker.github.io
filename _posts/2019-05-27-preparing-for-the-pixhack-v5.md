---
layout: post
title: "Preparing for the PixHack v5"
---

For many years I have wanted to work on developing an autonomous helicopter but have constantly put it off for numerous reasons (excuses). Finally in 2018 I made the leap and bought a Blade 360 CFX helicopter. Since then I have learned (with plenty of crashes) how to operate it. While I don't consider myself a great pilot, I *think* I can fly sufficiently well enough to gather some useful flight data. Thus I did some research and I came to the conclusion the [PixHack v5](http://ardupilot.org/copter/docs/common-pixhackV5-overview.html) flight controller would be the best option due to its built in sensor isolation. Furthermore, I have decided to utilize [ArduPilot](http://ardupilot.org/) as the community has active work with traditional helicopters whereas DroneCode/PixHawk seems heavily biased towards quadcopters and the like.

![blade 360]({{site.baseurl}}/images/general/blade-360-cfx.jpg){:width="90%"}

Since ordering the new piece of hardware I have started to setup my development environment on my laptop which runs on Windows 10 by following the directions [here](http://ardupilot.org/dev/docs/building-setup-windows10.html#building-setup-windows10). Given my intent of working with a traditional helicopter I switched to **Copter-3.6**.

The location of the environment setup script referenced in the instructions was out of date:
```
./Tools/environment_install/install-prereqs-ubuntu.sh -y
```
Should now be:
```
./Tools/scripts/install-prereqs-ubuntu.sh -y
```
## Building with Waf
With the environment properly configured the Waf build process was tested as follows.
