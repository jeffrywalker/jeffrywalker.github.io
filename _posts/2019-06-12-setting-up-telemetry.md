---
layout: post
title: "Setting Up Telemetry"
published: true
---

![armedTelem]({{site.baseurl}}/images/telemsetup/armed.jpg){:width="90%"}

Telemetry allows live data to be transmitted from the PixHack to the RC Radio and/or the ground station. This provides useful information such as the armed status, active flight mode, battery level, aircraft state information (attitude, velocities, ...), etc.

Setting up telemetry on the PixHack was relatively straight forward, that is after I realized the [FrySky Yaapu telemetry cable](https://www.amazon.com/Telemetry-Converter-Pixhawk-Taranis-Receiver/dp/B07KJFWTCB) was not properly wired for the PixHack connection. (I may have glazed over that it stated it connected to PixHawk 1,2,3,4 ...I mean why would anyone want to change the pin connection order, right?) Comparing the pinout of the [PixHawk 4](http://www.holybro.com/manual/Pixhawk4-Pinouts.pdf) to that of the [PixHack pinout](http://ardupilot.org/copter/_images/v5-pinouts_release.jpg) it became clear that some wiring was needed to be changed.

![wiringfix]({{site.baseurl}}/images/telemsetup/wiringfix.jpg){:width="90%"}

With the wiring connections fixed and the telemetry for SERIAL4_PROTOCOL set to 10 (FrySky S.Port Pass Through) the radio properly received telemetry data. The WiFi telemetry was connected to the TELEM1 port (SERIAL1) with the MavLink1 protocol, this enabled my surface pro to get the same data when connected to the helicopter's CUAVPWLINK (default password: cuavpwlink).

![disarmedTelem]({{site.baseurl}}/images/telemsetup/disarmed.jpg){:width="90%"}