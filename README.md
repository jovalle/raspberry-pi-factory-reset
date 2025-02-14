# Factory reset your Pi

:warning: Factory-resetting will delete any data off the root partition during
restoration. :warning:

## Description

If you regularly need to reset or restore a Raspberry Pi, it can become a bit
annoying to have to power down the rPi, unplug the sdcard, and re-flash the
original image back again.

This project modifies the vanilla Pi OS
[images](https://github.com/limepepper/raspberry-pi-factory-reset/wiki/Downloads)
to add a `/boot/factory_reset` utility and a
recovery partition containing a pristine image, which can be reset remotely
with a single command.

The most basic usage is that when you want to factory reset the pi, is to to
run the following command from the image:

    root@raspberrypi:~# /boot/factory_reset --reset

It support some other options to preserve various settings

    root@raspberrypi:~# /boot/factory_reset
    usage: /boot/factory_reset options
    Calling this script causes the rPi to reboot and factory reset. All data is lost

    OPTIONS:
      --reset                set this option to proceed with reset,
                              otherwise script will exit and do nothing

      --copy-pi-password     during the reset, preserve the pi user password

      --copy-root-password   during the reset, preserve the root password

      --copy-wifi            preserve the current wifi settings



The factory reset causes the rPi to reboot to a recovery partition, upon which
it restores the original root partition, and then reboots back to the fresh
installation (all without user intervention).

### Ready to use images

These Pi OS/raspbian images can be directly flashed and run:

https://github.com/limepepper/raspberry-pi-factory-reset/wiki/Downloads


## Usage

### Resetting the rPi back to factory state

Once the restore image is flash and the pi is booted, it will work as a normal
Pi OS/raspbian installation.

For example you could do the following (over ssh) from the rPi to cause a
factory reset:

    root@raspberrypi:~# /boot/factory_reset --reset
    factory restore script
    resetting
    rebooting...
    Connection to raspberrypi.local closed by remote host.
    Connection to raspberrypi.local closed.

The Pi will restore to a fresh installation:

![GitHub Logo](/assets/images/raspi-restore-screenshot_300px.png)

The pi will then reboot back to a fresh installation of Raspbian. The script
sets up the restored raspbian so ssh is running and available.

### Note on image sizes

These zipped images contain a copy of the original root partition, a pristine
copy of the rootfs, and a recovery partition. So they are at least 2 times the
original size.

### Other information

[Building your own images](https://github.com/limepepper/raspberry-pi-factory-reset/wiki/Build-your-own-images)

[Background](https://github.com/limepepper/raspberry-pi-factory-reset/wiki/Background)





Warning
-------

Obviously factory resetting a device is a destructive process, so don't try this
unless you understand what you are doing.

License
-------

The code is provided as is, and can be used/modified for any purpose, attribution
is appreciated but not required.

Sources/References
----

This project was inspired by a blog post on binarycents.com, but that site appears
to be gone now:
http://www.binarycents.com/raspberry-pi/raspberry-pi-remote-reinstall/


Some other sources of information:

https://raspberrypi.stackexchange.com/questions/80070/remote-full-reset-re-install-of-a-raspberry

There is some more information about the process in these blog posts:

* https://limepepper.co.uk/raspberry-pi/2018/04/15/Remote-factory-reset-for-raspberry-pi-1.html
* https://limepepper.co.uk/raspberry-pi/2018/04/16/Remote-factory-reset-for-raspberry-pi-2.html

