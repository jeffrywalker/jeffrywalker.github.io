---
layout: post
title: "RC Heli Setup"
---
Originally, I had planned to conduct some test flights to record data while flying with the original flybarless control unit. However, during the course of setting up the telemetry connections I decided there wasn't much to gain from doing that and so opted to finish setting up the PixHack for RC Heli flight.

To begin with I started to use [QGround Control](http://qgroundcontrol.com/) (QGC) instead of Mission Planner as the ground control software used to update the onboard parameters. I then followed the helicopter setup information found on the [ArduPilot documentation page](http://ardupilot.org/copter/docs/traditional-helicopter-configuration.html).

I then read the brief description of the control laws and tuning recommendations found [here](http://ardupilot.org/copter/docs/traditional-helicopter-tuning.html). Connecting the heli up to QGC I adjusted the parameters to match the values listed. In some cases this required a manual override in order to set the I/D gains to zero. NOTE: as I am using ArduCopter 3.6.9 the parameter RC_FEEL no longer exists and has been replaced with ATC_INPUT_TC (0.5=Very Soft, 0.2=Soft, 0.15=Medium, 0.1=Crisp, 0.05=Very Crisp). At this point I was eager to spool up the heli and inadvertently skipped the [Pre-Flight Testing](http://ardupilot.org/copter/docs/trad-heli-preflight-testing.html) which would have been useful.

## Test Flight: 001
**Goal:** 
establish the required yaw control gain.

**Remarks:**
* late evening with rain, conducted test indoors
* motor never spooled up to expected RPM
* suspect cyclic controls are inverted

**Post Flight:**

The transmitter throttle channel never exceeded a PWM of 1200; looking at the original transmitter setting for NORMAL mode the throttle curve should correspond to a value of 50%. After inspecting the throttle curved I inherited from the internet I adjusted the curve to ramp from zero at zero collective to 50% at mid-full collective. 

At this point I wanted to confirm what RC value was received on the throttle channel as well as what was sent to the ESC. To view the log data I first used Mission Planner; however, the interface left a lot to be desired. After some brief Googling I came across the [ardupilog](https://github.com/Georacer/ardupilog) project which provided a convenient MATLAB interface (which I plan on expanding for my needs).

## Test Flight: 002
**Goal:** 
establish the required yaw control gain.

**Remarks:**
* motor spooled up, potentially faster than required
* forgot to check cyclic controls, flight controller flipped the helicopter
* REPLACE: main rotors, flybarless linkages

At this point it was clear I had forgotten to verify the cyclic control directions as they were reversed. I knew this was the case as I had reversed the collective direction when following the setup videos. However, at the time I didn't check the cyclic directions. To properly fix this issue I set SERVO[01-03]\_REVERSED to be reversed and then reset the collective direction to be NORMAL.

## Test Flight: 003
**Goal:** 
establish the required yaw control gain.

**Remarks:**
* didn't attempt to hover
* heli was stable at full head speed