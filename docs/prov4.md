# Setting up the PTP server

[Back to Provisioning Overview](provisioning.md){.md-button}

[Precision Time Protocol (PTP)](https://en.wikipedia.org/wiki/Precision_Time_Protocol) is used to synchronise clocks throughout a network. The ADAPT payload uses this technology because it can achieve accuracy at the sub-microsecond range. The cameras in use on the ADAPT payload accept PTP (IEEE 1588) packets to ensure the images have extremely accurate time stamps.

configure ptp4l
```
sudo systemctl stop ptp4l
sudo nano /etc/linuxptp/ptp4l.conf
# add/edit the lines below
```
/etc/linuxptp/ptp4l.conf
```
tx_timestamp_timeout    10
```
Start ptp4l and review status
```
sudo systemctl start ptp4l
sudo systemctl status ptp4l
```

We would expect to see something similar to the output shown below:
```
ptp4l[1642.768]: port 1: INITIALIZING to LISTENING on INITIALIZE
ptp4l[1642.768]: port 0: INITIALIZING to LISTENING on INITIALIZE
ptp4l[1642.769]: port 1: link up
ptp4l[1648.777]: port 1: LISTENING to MASTER on ANNOUNCE_RECEIPT_TIMEOUT_EXPIRES
ptp4l[1648.777]: selected best master clock 48b02d.fffe.3a7004
ptp4l[1648.777]: assuming the grand master role
```
Note: the "assuming grand master role" line.  This means we will be serving the time to the clients on the network.

[Next Step](prov5.md){.md-button}