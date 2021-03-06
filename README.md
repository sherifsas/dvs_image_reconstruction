# DVS Image Reconstruction 
**Cedric Scheerlinck**

This repository contains **(1) Complementary filter** (combines events and frames) and **(2) High pass filter** (pure event reconstruction). It can be used to reconstruct a continuous-time image representation of the event stream.

![filter_pic](images/filter.png)

This package was developed using ROS version [Kinetic](http://wiki.ros.org/kinetic) (Ubuntu 16.04).
It can be run in real-time using **(1) live [DVS](https://inivation.com/dvs/)** ([RPG Event Camera Driver](https://github.com/uzh-rpg/rpg_dvs_ros)), or **(2) pre-recorded rosbag** ([data](https://drive.google.com/drive/folders/1Jv73p1-Hi56HXyal4SHQbzs2zywISOvc?usp=sharing), **[Color Event Dataset](http://rpg.ifi.uzh.ch/CED.html)**). Got a noisy rosbag? Try the [hot pixel filter](https://github.com/cedric-scheerlinck/dvs_hot_pixel_filter).

The source code is released under the **MIT License**.

### Publication

If you use this work in an academic context, please cite the following work  ([PDF](https://cedric-scheerlinck.github.io/files/2018_scheerlinck_continuous-time_intensity_estimation.pdf), [BibTex](https://cedric-scheerlinck.github.io/files/2018_accv_continuous_bibtex.txt)):

* Cedric Scheerlinck, Nick Barnes, Robert Mahony, "Continuous-time Intensity Estimation Using Event Cameras", Asian Conference on Computer Vision (ACCV), Perth, 2018.

## Install Instructions

Please replace \<YOUR VERSION\> with your [ROS](http://wiki.ros.org/ROS/Installation) version (e.g. kinetic).

Install [libusb](https://libusb.info/), [catkin tools](http://catkin-tools.readthedocs.org/en/latest/installing.html), [vcstool](https://github.com/dirk-thomas/vcstool) and autoreconf:

    sudo apt install libusb-1.0-0-dev python-catkin-tools python-vcstool dh-autoreconf
    
Install ROS dependencies:

    sudo apt install ros-<YOUR VERSION>-camera-info-manager ros-<YOUR VERSION>-image-view
    
Create a new catkin workspace if needed:

    mkdir -p ~/catkin_ws/src && cd ~/catkin_ws/
    catkin config --init --mkdirs --extend /opt/ros/<YOUR VERSION> --merge-devel --cmake-args -DCMAKE_BUILD_TYPE=Release

Clone this repository:

    cd src/
    git clone https://github.com/cedric-scheerlinck/dvs_image_reconstruction.git

Clone dependencies:

    vcs-import < dvs_image_reconstruction/dependencies.yaml
    
Add udev rule to run live [DVS](https://inivation.com/dvs/) (see [RPG Event Camera Driver](https://github.com/uzh-rpg/rpg_dvs_ros)):

    cd rpg_dvs_ros/libcaer_catkin/
    sudo ./install.sh

Build the packages:  

    catkin build davis_ros_driver complementary_filter pure_event_reconstruction
    source ~/catkin_ws/devel/setup.bash

## Downloads
Datasets can be found [here](https://drive.google.com/drive/folders/1Jv73p1-Hi56HXyal4SHQbzs2zywISOvc?usp=sharing).  
The **[Color Event Dataset](http://rpg.ifi.uzh.ch/CED.html)** containing color frames and events is now available!

## Video
[![dvs_image_reconstruction_video](images/thumbnail_combined.png)](https://youtu.be/bZ0ZKido0Ag)
[https://youtu.be/bZ0ZKido0Ag](https://youtu.be/bZ0ZKido0Ag)

## Website

The webpage for this project with links to data, slides, paper and more can be found here:

[https://cedric-scheerlinck.github.io/continuous-time-intensity-estimation](https://cedric-scheerlinck.github.io/continuous-time-intensity-estimation)

## Acknowledgements

This research was funded by an Australian Government Research Training Program Scholarship (AGRTP) and the Autralian Research Council through the Australian Centre of Excellence for Robotic Vision ([ACRV](https://www.roboticvision.org/)) CE140100016.
