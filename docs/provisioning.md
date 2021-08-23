# Provisioning Guide

This guide walks a user through the steps of setting up software on the computer in order to have the ADAPT payload perform realtime analytics. Please note that some of the software used is subject to change and may need adjustments per platform. The guide is initially meant to work primarily on NVIDIA's Tegra hardware, but should represent steps that would be very similar, if not the same, on other hardware platforms.

## Simulation vs. Live Hardware

The guide below is meant to run on [live hardware](parts.md). If you would like to get started with a simulated setup, [start here](https://gitlab.kitware.com/adapt/adapt/-/tree/master/AirSim) instead.

## Initial flashing

Follow NVIDIA's [documentation on the initial flashing](https://docs.nvidia.com/jetson/l4t/){target=_blank}or start by using the [NVIDIA SDK Manager](https://developer.nvidia.com/nvidia-sdk-manager){target=_blank}.

## Installing ROS

The [Robot Operating System (ROS)](https://www.ros.org/) is used by the ADAPT payload for communications, logging, and more. Follow [these steps](http://wiki.ros.org/melodic/Installation/Ubuntu){target=_blank} to get ROS installed.

## Getting the ADAPT software stack

Follow [these steps](prov1.md) to setup prerequisite software and the open source ADAPT ROS software stack.

## Setting up 1PPS hardware input

The ADAPT payload uses a [One Pulse Per Second (1PPS)](https://en.wikipedia.org/wiki/Pulse-per-second_signal) input from the GPS sensor in order to synchronize the time on the system, sensors, and cameras as accurately as possible. Follow [these steps](prov2.md) to get 1PPS working.

## Configuring the time server

In order to make the ADAPT computer capable of serving time to the camera(s), [chrony](https://chrony.tuxfamily.org/) is used along with [gpsd](https://gpsd.gitlab.io/gpsd/). Follow [these steps](prov3.md) to get the time server setup.

## Setting up the PTP server

[Precision Time Protocol (PTP) or IEEE 1588](https://en.wikipedia.org/wiki/Precision_Time_Protocol) is a way to synchronize clocks throughout a network. Follow [these steps](prov4.md) to get PTP setup.

## Configuring automatic startup

Follow [these steps](prov5.md) to get the PTP and ADAPT software stacks running automatically when the computer boots up.

## Setting up the Basestation User Interface

Steps to setup a docker container with a User Interface (UI) for remotely monitoring/controlling the ADAPT software can be found [here](https://gitlab.kitware.com/adapt/adapt_ros_ws/-/tree/master/basic_ui).