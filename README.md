# Project

This projects aims to provide an AOSP build system capable of boot with Linux Mainline kernel on the Oneplus 5 (Cheeseburger).

At the moment, AOSP (Android S) is validated to boot with Kernel 5.10.
Kernel sources are available here:
https://github.com/robertosartori/mainline-kernel-oneplus-msm8998

# Build instructions
Follow the instructions from Google to setup a machine to build Android 11:
https://source.android.com/setup/build/initializing

Then, sync all the sources:
```
$ repo init -u https://github.com/roberto-sartori-gl/mainline-manifest -b msm8998/android-mainline-5.10 -m cheeseburger.xml
$ repo sync -c --no-clone-bundle --no-tags
```
then:
```
$ source build/envsetup.sh
$ lunch cheeseburger-userdebug
$ make -j12
```
the images will be available in `out/target/product/cheeseburger`.

# Flash instructions
The images can be flashed using fastboot:
```
$ fastboot flash boot out/target/product/cheeseburger/boot.img
$ fastboot flash system out/target/product/cheeseburger/system.img
$ fastboot flash vendor out/target/product/cheeseburger/vendor.img
$ fastboot flash userdata out/target/product/cheeseburger/userdata.img
```

# Current status
Following features are working:
- display (upside down at the moment)
- touch
- bluetooth
- volume and power buttons
- adb for debug
- RTC
- Brightness control

# ToDo
Following features are not working:
- screen orientation (upside down at the moment)
- audio (no driver and no device tree nodes)
- battery stats
- fingerprint and capacitive buttons
- wifi (it turns on but it is not possible to connect to any wifi network)
- RIL (2g/3g/4g, phone calls)
- suspend (when screen goes off, bluetooth and adb stop working)
- RGB LED
- haptics (https://wiki.postmarketos.org/wiki/Haptics)
- Cameras
- NFC

# Thanks to...
I mostly put the pieces together. So thanks to:
- Jami Kettunen for the effort to get the OnePlus 5 to work on the mainline kernel: https://github.com/JamiKettunen/linux-mainline-oneplus5
- SoMainline guys, in particular kholk for the work on the msm8998 platform: https://github.com/SoMainline/linux
- The guys from postmarketOS: https://wiki.postmarketos.org/wiki/OnePlus_5_(oneplus-cheeseburger)
- trautamaki, for the mainline branch where I started: https://github.com/trautamaki/android-mainline_kernel_oneplus_msm8998
