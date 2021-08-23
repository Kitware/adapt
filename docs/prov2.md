# Setting up 1PPS hardware input

[Back to Provisioning Overview](provisioning.md){.md-button}

Setup the device tree overlay:
```
sudo nano /boot/pps.dts
# copy and paste the code below:
```
/boot/pps.dts
```
/dts-v1/;
/plugin/;

/ {
    overlay-name = "Jetson PPS";
    compatible = "p2822-0000+p2888-0001,p2972-0000-devkit,devboard";
    fragment {
        target-path = "/";
        __overlay__ {
                        pps: pps_gpio {
                                compatible = "pps-gpio";
                                gpios = <&tegra_main_gpio 56 1>;
                                status = "okay";
                        };
        };
    };
};
```

compile the dts:
```
cd /boot
sudo dtc -I dts -O dtb -@ -o pps.dtbo pps.dts

# it give may show some warnings:
# pps.dtbo: Warning (gpios_property): Property 'gpios', cell 1 is not a phandle reference in /fragment/#__overlay__/pps_gpio
# pps.dtbo: Warning (gpios_property): Could not get phandle node for /fragment/__overlay__/pps_gpio:gpios(cell 1)
```

Setup the overlay dtb file
```
sudo fdtoverlay -i tegra194-p2888-0001-p2822-0000.dtb -o tegra194-p2888-0001-p2822-0000-user-custom.dtb tegra194-p2888-0001-p2822-0000-hdr40.dtbo pps.dtbo
```

Edit the /boot/extlinux/extlinux.conf
```
sudo nano /boot/extlinux/extlinux.conf
# insert the new line between the INITRD and APPEND lines as shown below
```

/boot/extlinux/extlinux.conf
```
    LINUX ...
    INITRD ...
    FDT /boot/tegra194-p3668-all-p3509-0000-user-custom.dtb
    APPEND ...
```

Configure the hardware:
```
sudo /opt/nvidia/jetson-io/config-by-hardware.py -n "Jetson PPS"
# it should say:
# Configuration saved to /boot/tegra194-p2888-0001-p2822-0000-jetson-pps.dtb.
```

Now reboot and you should see a pps device with this command
```
ls /dev/ | grep pps
```
(that should show /dev/pps0)

Confirm that the signal is coming in:
```
dmesg --follow --ctime | grep capture
```
With that command issued you should see one message every second, similar to this:
```
[Mon May 31 09:50:54 2021] pps pps0: capture assert seq #2760932
[Mon May 31 09:50:55 2021] pps pps0: capture assert seq #2760933
[Mon May 31 09:50:56 2021] pps pps0: capture assert seq #2760934
[Mon May 31 09:50:57 2021] pps pps0: capture assert seq #2760935
[Mon May 31 09:50:58 2021] pps pps0: capture assert seq #2760936
```

[Next Step](prov3.md){.md-button}