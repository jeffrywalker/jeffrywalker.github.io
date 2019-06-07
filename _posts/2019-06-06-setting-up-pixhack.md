layout: post
title: "Setting Up the PixHack"
---

After some procrastination I got around to setting up the PixHack and related items such as the Taranis QX7S radio. For reference my development machine runs Windows 10 and have opted to install [Mission Planner (MP)](http://ardupilot.org/planner/) as my ground station software. As a side note I also have a Surface Pro 6 which I have installed MP on and intend to use when more convenient than my cumbersome laptop. 

# Radio Setup
Unlike the Spektrum radio I have used in the past the Taranis radio did not come with any voice packs pre-loaded. As the Taranis runs on OpenTX the first step was to install the [companion software](https://www.open-tx.org/2019/01/06/opentx-2.2.3). Additionally, the *SDCard* content for 2.2.3 was also downloaded, specifically [this](https://downloads.open-tx.org/2.2/release/sdcard/opentx-x7/sdcard-taranis-x7-2.2V0018.zip). Since there was an option I went ahead and customized the splash screen...

![splashscreen]({{site.baseurl}}/images/radio/splashscreen.jpg){:width="90%"}

I then binded the radio to the RX in Mode 5 which required no jumpers during the bind process (though the F/S button was held during power-up).