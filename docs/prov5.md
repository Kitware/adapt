# Configuring automatic startup

[Back to Provisioning Overview](provisioning.md){.md-button}

The installation of the [ADAPT ROS Workspace](https://gitlab.kitware.com/adapt/adapt_ros_ws) contains a folder with example configuration files.  Among those are some systemd service files. NOTE: you may want to edit the paths inside the two files shown below to match where your 'adapt_ros_ws' files are located.

To install the systemd service files, follow these commands:
```
cd adapt_ros_ws/example_config/
sudo cp adapt_ptp_stack.service /etc/systemd/system/
sudo cp ros_stack.service /etc/systemd/system/
sudo systemctl daemon-reload
```

Now, when you reboot the two services should be running automatically. You can check on the status with these commands:
```
sudo systemctl status adapt_ptp_stack
sudo systemctl status ros_stack
```

In addition, you can connect to the services with tmux and observe/change any operations with these commands:
```
sudo tmux a -t adapt_live
sudo tmux a -t adapt_ptp
```

In the tmux window you can use these key cominations to move between windows, etc.:
```
# move to the next window:
# ctr-b n

# move to the previous window:
# ctrl-b p

# detach from session
# ctrl-b d
```

## Optional items: configure network addresses for ethernet devices

For the standard ADAPT software we are assuming the camera is on this network:
```
169.254.251.x
```
and the Wireless communications are on this network
```
100.0.0.x
```

[Back to Provisioning](provisioning.md){.md-button}