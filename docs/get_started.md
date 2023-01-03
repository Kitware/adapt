
# Getting started with ADAPT

The ADAPT payload source code is hosted here: [https://gitlab.kitware.com/adapt/adapt_ros_ws](https://gitlab.kitware.com/adapt/adapt_ros_ws).


# Trying ADAPT without any hardware

There is also another way to explore the ADAPT processing software without requiring a flyable ADAPT payload here: [ADAPT Processing of AirSim Data](https://gitlab.kitware.com/adapt/adapt/-/tree/master/doc/airsim_docker.md). This tutorial uses [Microsoft AirSim](https://microsoft.github.io/AirSim/) as a drone sensor emulator running alongside ADAPT processes within a fully Dockerized environment. Camera images along with associated ground-truth depth and semantic segmentation images are rendered and saved to disk as you navigate a simulated drone with your keyboard through a forested mountain landscape. The pairing of raw imagery with ground truth allows training a semantic segmentation deep-neural-network model using ADAPT training tools. Finally, the trained model is deployed to process AirSim imagery in real time.
