---
layout: post
title: "Setting Up the PixHack"
---

After some procrastination I got around to setting up the PixHack and related items such as the Taranis QX7S radio. For reference my development machine runs Windows 10 and have opted to install [Mission Planner (MP)](http://ardupilot.org/planner/) as my ground station software. As a side note I also have a Surface Pro 6 which I have installed MP on and intend to use when more convenient than my cumbersome laptop. 

# Radio Setup
Unlike the Spektrum radio I have used in the past the Taranis radio did not come with any voice packs pre-loaded. As the Taranis runs on OpenTX the first step was to install the [companion software](https://www.open-tx.org/2019/01/06/opentx-2.2.3). Additionally, the *SDCard* content for 2.2.3 was also downloaded, specifically [this](https://downloads.open-tx.org/2.2/release/sdcard/opentx-x7/sdcard-taranis-x7-2.2V0018.zip). Since there was an option I went ahead and customized the splash screen...

![splashscreen]({{site.baseurl}}/images/radio/splashscreen.jpg){:width="90%"}

I then binded the radio to the RX in Mode 5 which required no jumpers during the bind process (though the F/S button was held during power-up).

## OpenTX Setup
A convenient feature of OpenTX is the ability to configure model radio settings on the computer using the Companion software instead the more cumbersome interface on the radio. To begin with I imported a model I found online for a similar albeit smaller helicopter than mine [Blade 180CFX radio file](https://rcsettings.com/index.php/viewdownload/4-helicopters/317-blade-180cfx). 

### Volume Setting
Though S1 was configured to control the volume on the radio, it was set such that the volume is MAX when HOLD mode is inactive. While this makes sense during flight, the voice became annoying during the setup procedure, so I disabled this setting.

### Output Channel Order
The nominal output channel order for the Blade/Spektrum lineup is different than what is required for the [ArduPilot interface](http://ardupilot.org/copter/docs/traditional-helicopter-connecting-apm.html#overview-of-servo-and-rx-connection).

| Channel   | Blade/Spektrum    | ArduPilot     |
| ---       | ---               | ---           |
| 1         | Throttle          | Roll          |        
| 2         | Roll              | Pitch         |
| 3         | Pitch             | Collective    |        
| 4         | Yaw               | Yaw           |
| 5         | Gyro              | FlightMode    |        
| 6         | Collective        | Tuning        |    
| 7         | Aux2              | Aux           |
| 8         | Aux3              | Throttle      |    

### RC Calibration
Using MP the radio was calibrated and the parameters were written to PixHack. This is an important step to ensure full range of controls.

![radio-calibration]({{site.baseurl}}/images/radio/radio-calibration.jpg)

### Board Orientation
Since the PixHack is mounted upside down on the helicopter the board orientation was set to ROLL180. With this parameter adjusted the *Write Params* button was pressed sending the changes to the PixHack.

![board-orientation]({{site.baseurl}}/images/radio/board-orientation.jpg)


### Accelerometer Calibration
Once the board orientation was setup it was time to calibrate the accelerometers. This process establishes the range of values that will be seen during flight by holding the aircraft in the following orientations: level, left, right, nose down, nose up, back.

### Compass Calibration
The compass calibration was carried out using the [Onboard Calibration](http://ardupilot.org/copter/docs/common-compass-calibration-in-mission-planner.html#onboard-calibration) method. This process consisted of holding the helicopter in the various orientations used during the acceloremeter calibration at each heading (N, S, E, W). Once the calibration was completed the PixHack was rebooted.

![compass-calibration]({{site.baseurl}}/images/radio/compass-calibration.jpg)

# Next Steps
At this juncture the PixHawk is now ready to start capturing data during flight using the original controller and radio. In order to utilize the PixHack during flight I will need to follow the remaining setup process for configuring helicopter specific gains and parameters as outlined on the [ArduPilot Helicopter Ground School page](http://ardupilot.org/copter/docs/traditional-helicopter-configuration.html#). This process will be postponed as I first want to capture some flight data and ensure the quality is satisfactory prior to committing to flying with the new hardware. 