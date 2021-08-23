# Configuring the time server

[Back to Provisioning Overview](provisioning.md){.md-button}

## Recommended (optional) steps: setting up the hardware device names

For the ADAPT payload software, we use /dev/gps and /dev/spatial as names for the NMEA and Advanced Navigation Spatial hardware names (this avoids issues with ttyUSB0/1/2 etc. numbering).  In order to set this up, you'll need to know the device IDs - usually found with the 'lsusb' command.  For reference, the USB hardware we used look like this:
```
lsusb
067b:2303 Prolific Technology, Inc. PL2303 Serial Port   # <- this is the 9-pin serial to USB converter
0403:6001 Future Technology Devices International, Ltd FT232 USB-Serial (UART) IC  # <- this is the standard Spatial USB cable
```
Setup the udev rule
```
sudo nano /etc/udev/rules.d/99-zgps.rules
# copy and paste the info below (after changing the IDs to match your hardware)
```
/etc/udev/rules.d/99-zgps.rules
```
SUBSYSTEM=="tty", ATTRS{idVendor}=="067b", ATTRS{idProduct}=="2303", GROUP="dialout",  SYMLINK+="gps"
SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", GROUP="dialout", SYMLINK+="spatial"
```
Reload the udev rules to see /dev/gps and /dev/spatial
```
udevadm control --reload-rules && udevadm trigger
```

## Required steps: configuring gpsd and chronyd

Disable the standard timesync
```
sudo systemctl stop systemd-timesyncd.service
sudo systemctl disable systemd-timesyncd.service
```
Disable standard gpsd startup since we may need to run it in debug mode
```
sudo systemctl stop gpsd
sudo systemctl disable gpsd
sudo systemctl stop gpsd.socket
sudo systemctl disable gpsd.socket
```
If you do need to run it in debug mode, issue these commands to test it and see output
```
sudo killall gpsd
sudo gpsd -D 5 -N -n -b /dev/gps /dev/pps0
```
note: the ADAPT payload software will start gpsd (refer to [this](https://gitlab.kitware.com/adapt/adapt_ros_ws/-/blob/master/run_scripts/ptp/10_gpsd.sh) for reference)

Configure chrony
```
sudo systemctl stop chronyd
sudo nano /etc/chrony/chrony.conf
# add/edit lines as shown below
```
/etc/chrony/chrony.conf
```
allow
# rtcsync  # note: turn this off to not use system clock
refclock SHM 0 refid GPS precision 1e-1 offset 0.045 noselect
refclock SHM 2 refid PPS precision 1e-7 prefer
```
Start chrony and review the sources
```
sudo systemctl start chronyd
chronyc sources
```
we want the PPS and GPS to show like this:
```
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
#- GPS                           0   4   377    12  +3580us[+3580us] +/- 101ms
#* PPS                           0   4   377    10    -86ns[ -157ns] +/- 181ns
```
Note: the * next to PPS

[Next Step](prov4.md){.md-button}