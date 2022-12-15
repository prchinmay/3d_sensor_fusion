# 3d_sensor_fusion

## Overview 

This contains solution for course (RO47004) project of TU Delft masters robotics program. It relates to processing data 
coming from LIDAR and camera sensors placed on a moving vehicle and visualize them on a common reference frame. 

![gif](pics/record.gif)

## Context

### Data provided
Practicum, you are provided with a (tiny) sample of this [dataset](https://eurocity-dataset.tudelft.nl/), consisting of:

* Ego-motion odometry measurements at different times t, namely the velocity vt and the
steering rate t. These measurements are recorded at a frequency of 50 Hz.

* Vision data from a stereo camera installed behind the windshield. This data has already
been processed so you can work with the left rectified RGB image and the corresponding
disparity image. Further, the camera parameters such as the baseline, the focal length
and the image center are given.

* 3D point cloud data from a LiDAR sensor that contain a 360-degree sweep of the environment
around the vehicle.

* The static transformations of the two sensors with respect to the vehicle coordinate system
are given as translation and rotation in 3D.

### Task
Below is a schematic of the incoming data over time. Since the vehicle has moved between measurements, the data
requires to compensate for this ego-motion to properly align the sensor data. In this assignment,
the data is processed and visualized in a common reference frame.

![frame](pics/frame.PNG)
![lidar1](pics/lidar1.PNG)
![lidar2](pics/lidar2.png)
![calib](pics/calib.PNG)
![compensated](pics/compensated.png)
![stereo1](stereo1.PNG)
![stereo2](stereo2.PNG)
![gif](pics/record.gif)

![gif](pics/record.gif)


![lidar_angles](pics/lidar_angles.PNG)