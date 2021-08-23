# Getting the ADAPT software stack

[Back to Provisioning Overview](provisioning.md){.md-button}

Below is a step-by-step explanation if you want to follow along or you can run this as a single script from [here](https://gitlab.kitware.com/adapt/adapt_ros_ws/-/blob/master/example_config/1_adapt_software.sh).

1. Install OS prerequisites:
```
sudo apt update
sudo apt install dirmngr gnupg2 python-catkin-tools python-pip python-tk python-rosdep python-rosinstall \
    python-vcstools ros-melodic-ros-core=1.4.1-0* ros-melodic-ros-base=1.4.1-0* ros-melodic-perception=1.4.1-0* \
    ros-melodic-rqt-image-view libgl1-mesa-glx libqt5x11extras5 gdal-bin python-gdal python-ujson \
    cuda-toolkit-10-2 cuda-core-10-2 libcudnn8-dev tensorrt tmux libhdf5-serial-dev hdf5-tools libhdf5-dev \
    zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran gpsd chrony pps-tools linuxptp \
    nvidia-tensorrt python-libnvinfer-dev libopenblas-base libopenmpi-dev

```

2. Install python prerequisites:
```
# NOTE: install these dependencies as root so the systemd process can find them instead of a user account
sudo pip install anaconda ipython ipykernel matplotlib spyder-kernels protobuf \
    PyGeodesy shapely pyshp simplekml exifread future yacs scipy psutil pycuda
sudo pip install Pillow --upgrade
```

3. Get this version of pytorch for tegra from NVIDIA:
```
cd ~
wget https://nvidia.box.com/shared/static/yhlmaie35hu8jv2xzvtxsh0rrpcu97yj.whl -O torch-1.4.0-cp27-cp27mu-linux_aarch64.whl
sudo pip install future torch-1.4.0-cp27-cp27mu-linux_aarch64.whl
```

4. Setup torchvision
```
cd ~
git clone https://github.com/pytorch/vision
cd vision
git fetch origin v0.5.0
git reset --hard FETCH_HEAD
sudo python setup.py install
```

5. Setup a specific version of torch2trt:
```
cd ~
git clone https://github.com/NVIDIA-AI-IOT/torch2trt.git
cd torch2trt
git fetch origin b0cc8e77a0fbd61e96b971a66bbc11326f77c6b5
git reset --hard FETCH_HEAD
sudo python setup.py install --plugins
```

6. Run the rc_genicam_api install
```
cd ~
git clone https://github.com/roboception/rc_genicam_api.git
cd rc_genicam_api
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX=/usr ..
make && make package
sudo dpkg -i rc-genicam-api*.deb
```

7. Setup the adapt ros workspace
```
cd ~
git clone https://gitlab.kitware.com/adapt/adapt_ros_ws.git
cd adapt_ros_ws
git submodule init
git submodule update
catkin build --force-cmake -DSETUPTOOLS_DEB_LAYOUT=OFF
# get the model
cd ~/adapt_ros_ws/models
./get_sim_model.sh
```

## OPTIONAL items

Clean up some disk space:
```
sudo apt-get remove --purge libreoffice*
sudo apt-get autoclean
sudo apt-get autoremove
```

jtop for system stats:
```
pip install -U jetson-stats
# run jtop
```

jetsonUtilities:
```
git clone https://github.com/jetsonhacks/jetsonUtilities
cd jetsonUtilities
python jetsonInfo.py
```

[Next Step](prov2.md){.md-button}