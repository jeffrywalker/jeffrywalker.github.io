---
layout: post
title: "Preparing for the PixHack v5"
---

For many years I have wanted to work on developing an autonomous helicopter but have constantly put it off for numerous reasons (excuses). Finally in 2018 I made the leap and bought a Blade 360 CFX helicopter. Since then I have learned (with plenty of crashes) how to operate it. While I don't consider myself a great pilot, I *think* I can fly sufficiently well enough to gather some useful flight data. Thus I did some research and I came to the conclusion the [PixHack v5](http://ardupilot.org/copter/docs/common-pixhackV5-overview.html) flight controller would be the best option due to its built in sensor isolation. Furthermore, I have decided to utilize [ArduPilot](http://ardupilot.org/) as the community has active work with traditional helicopters whereas DroneCode/PixHawk seems heavily biased towards quadcopters and the like.

![blade 360]({{site.baseurl}}/images/general/blade-360-cfx.jpg){:width="90%"}

Since ordering the new piece of hardware I have started to setup my development environment on my laptop which runs on Windows 10 by following the directions [here](http://ardupilot.org/dev/docs/building-setup-windows10.html#building-setup-windows10). Given my intent of working with a traditional helicopter I switched to **Copter-3.6**.

The location of the environment setup script referenced in the instructions was out of date:
```sh
./Tools/environment_install/install-prereqs-ubuntu.sh -y
```
Should now be:
```sh
./Tools/scripts/install-prereqs-ubuntu.sh -y
```
## Building with Waf
With the environment properly configured the Waf build process was tested as follows.
```sh
./waf configure --board CUAVv5
./waf copter
```
at this point I had to run
```sh
sudo apt install clang
```
and then retry building. This of course did not fix things but then I found [this](https://discuss.ardupilot.org/t/build-fails-with-wsl-on-windows-10/31555/2) which I tried 
```sh
subl ~/.profile
```
and remove the following line:
```
export PATH=/opt/gcc-arm-none-eabi-4_9-2015q3/bin:$PATH
```
and then run
```sh
sudo apt-get install gcc-arm-none-eabi -y
. ~/.profile
```
Unfortunately the gcc-arm-none-eabi install didn't complete properly, but scrolling down in the aformentioned post I read that the *master* was properly configured. So updated the following in the **install-prereqs-ubuntu.sh** script in order to match the master:
```sh
# GNU Tools for ARM Embedded Processors
# (see https://launchpad.net/gcc-arm-embedded/)
ARM_ROOT="gcc-arm-none-eabi-6-2017-q2-update"
ARM_TARBALL="$ARM_ROOT-linux.tar.bz2"
ARM_TARBALL_URL="http://firmware.ardupilot.org/Tools/STM32-tools/$ARM_TARBALL"
```
With this change the configuration and build process executed as expected:
```sh
:~/ardupilot$ ./waf configure --board CUAVv5
Setting top to                           : /home/ardupilot
Setting out to                           : /home/ardupilot/build
Autoconfiguration                        : enabled
Setting board to                         : CUAVv5
Checking for program 'arm-none-eabi-ar'  : /usr/bin/arm-none-eabi-ar
Using toolchain                          : arm-none-eabi
Checking for 'g++' (C++ compiler)        : /usr/bin/arm-none-eabi-g++
Checking for 'gcc' (C compiler)          : /usr/bin/arm-none-eabi-gcc
Checking for c flags '-MMD'              : yes
Checking for cxx flags '-MMD'            : yes
Checking for intelhex module:            : disabled
Checking for program 'make'              : /usr/bin/make
Checking for program 'arm-none-eabi-objcopy' : /usr/bin/arm-none-eabi-objcopy
Including /home/ardupilot/libraries/AP_HAL_ChibiOS/hwdef/fmuv5/hwdef.dat
Removing HAL_GPIO_A_LED_PIN
Removing HAL_GPIO_B_LED_PIN
Setup for MCU STM32F767xx
Writing hwdef setup in /home/ardupilot/build/CUAVv5/hwdef.h
Writing DMA map
Generating ldscript.ld
Checking for env.py
env set APJ_BOARD_TYPE=STM32F767xx
env set APJ_BOARD_ID=50
env set HAL_WITH_UAVCAN=1
env set FLASH_RESERVE_START_KB=32
env set CHIBIOS_BUILD_FLAGS=USE_FATFS=yes CHIBIOS_PLATFORM_MK=os/hal/ports/STM32/STM32F7xx/platform.mk CHIBIOS_STARTUP_MK=os/common/startup/ARMCMx/compilers/GCC/mk/startup_stm32f7xx.mk
Checking for HAVE_CMATH_ISFINITE             : yes
Checking for HAVE_CMATH_ISINF                : yes
Checking for HAVE_CMATH_ISNAN                : yes
Checking for NEED_CMATH_ISFINITE_STD_NAMESPACE : yes
Checking for NEED_CMATH_ISINF_STD_NAMESPACE    : yes
Checking for NEED_CMATH_ISNAN_STD_NAMESPACE    : yes
Checking for header endian.h                   : not found
Checking for header byteswap.h                 : not found
Checking for program 'python'                  : /usr/bin/python
Checking for python version >= 2.7.0           : 2.7.15
Checking for program 'python'                  : /usr/bin/python
Checking for python version >= 2.7.0           : 2.7.15
Source is git repository                       : yes
Update submodules                              : yes
Checking for program 'git'                     : /usr/bin/git
Gtest                                          : STM32 boards currently don't support compiling gtest
Checking for program 'arm-none-eabi-size'      : /usr/bin/arm-none-eabi-size
Benchmarks                                     : disabled
Unit tests                                     : disabled
Checking for program 'rsync'                   : /usr/bin/rsync
'configure' finished successfully (3.255s)
```
```sh
[517/520] Linking build/CUAVv5/lib/libArduCopter_libs.a
[518/520] Linking build/CUAVv5/bin/arducopter
[519/520] Generating bin/arducopter.bin
[520/520] apj_gen build/CUAVv5/bin/arducopter.bin

BUILD SUMMARY
Build directory: /ardupilot/build/CUAVv5
Target          Text    Data  BSS     Total
---------------------------------------------
bin/arducopter  987268  4148  389740  1381156

Build commands will be stored in build/CUAVv5/compile_commands.json
'copter' finished successfully (2m49.526s)
```