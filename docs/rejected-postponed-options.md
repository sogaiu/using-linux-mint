# Rejected / Postponed Options

Installing the following programs was considered but were either
rejected or postponed for various reasons.

## librewolf

Nice that it's Firefox-based without all of the meh of the current
Firefox, but it seemed a bit too extreme to work well for my uses.

https://librewolf.net/installation/debian/

Hoping things like LadyBird will be usable before too long.

## scrcpy

Packaged version of scrcpy seems too old.

May be better to not use...the scrcpy-server building seems to require
Android SDK to build.  Multiple distributions seem to just be using
the "prebuild" scrcpy-server...who knows whether the content is ok...

If revisiting, may want to look at
[this](https://github.com/Genymobile/scrcpy/blob/master/doc/build.md) and the following incomplete list of commands:

```
# gets the adb bits
sudo apt install scrcpy
# remove the old bits that don't appear to work
sudo apt remove scrcpy scrcpy-server
# runtime dependencies
sudo apt install ffmpeg libsdl2-2.0-0 adb libusb-1.0-0
# client build dependencies
sudo apt install gcc git pkg-config meson ninja-build libsdl2-dev \
                 libavcodec-dev libavdevice-dev libavformat-dev libavutil-dev \
                 libswresample-dev libusb-1.0-0-dev
# server build dependencies -- trying with 21
sudo apt install openjdk-17-jdk
# https://developer.android.com/studio/index.html#command-line-tools-only

cd ~/src
git clone https://github.com/Genymobile/scrcpy
cd scrcpy
# building scrcpy-server from source seems quite involved
```

