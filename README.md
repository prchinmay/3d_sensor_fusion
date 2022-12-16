# 3d_sensor_fusion

## Overview 

This contains solution for course (RO47004) project of TU Delft masters robotics program. It relates to processing data 
coming from LIDAR and camera sensors placed on a moving vehicle and visualize them on a common reference frame. 

![gif](pics/record.gif)

## Context

### Data provided
In the Practicum, we are provided with a (tiny) sample of this [dataset](https://eurocity-dataset.tudelft.nl/), consisting of:

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

## Solution

### 1. Ego-motion from odometry measurements

* A non-linear motion model $x_t+\Delta_t = f(x_t,m_t,\Delta_t)$ of the vehicle is provided below. A function is written
to implement a single step from t to t + $\Delta_t$ of the motion model. 
* This function is used to compute the relative 2D pose between the ego-vehicle’s poses at two times t_{from} and $t_{to}$. 
This transforms 3D points measured in one frame of reference at time $t_{from}$ to a reference frame at time $t_{to}$.

![motion_model](pics/motion_model.PNG)

### 2. 3D from LiDAR
* In below figure you see a point cloud from the LiDAR sensor of an ego-vehicle moving forward at about 10 m.
 The LiDAR scan starts in front of the ego-vehicle and from the bird-eye-view perspective rotates clockwise.

![compensated](pics/lidar1.PNG)
 
Given the scan frequency f and the capture time t of the last point at end of the 360 degree scan, the time 
$t_x$ when the point $x = (x, y, z)$ was captured is derived using:

<img src="pics/angle.PNG" width="400"/> <img src="pics/lidar_cal.PNG" width="400"/>

* The three subsequent point clouds after compensating the ego-motion in a single frame of reference looks like this

![lidar3](pics/lidar3.jpeg)

### 3. 3D from stereo vision

* Using the equations below, 3D positions (x, y, z) are computed per pixel from the disparity image with coordinates 
(u, v, d), given the camera information (focal length $f_x = f_y = f_{xy}$ with unit [pixels], image center 
$c_x, c_y$ ([pixels]) and the baseline b ([m]).

![calib](pics/calib.PNG)

* Using above equation, given the camera parameters for the original image and the disparity image, the 3D position for all 
valid pixels are computed. Pixels that have an infeasible 3D position due to the disparity value are set to np:nan.

* A left rectified camera image is provided as input. Using this, every associated point in the point cloud obtained from the 
stereo camera, is assigned a pixel value. Once this is done, the stereo cloud looks like the image below in two different 
views(front, top). 
  
<img src="pics/stereo1.PNG" width="400"/> <img src="pics/stereo2.PNG" width="400"/> 

### 4. 3D point cloud sensor alignment
* Currently, the points of both sensors are given in different reference frames, i.e. each in their own in sensor 
coordinate frame. You are given the sensor poses with respect to the vehicle frame of reference as translation and 
rotation. Use them to implement the function transform to car frame which should transform the points from
both sensor coordinates to a common coordinate frame, the coordinate frame of the vehicle. Additionally, compensate 
the ego-motion as the data of both sensors was captured at different times and if you have already implemented it, 
also compensate the ego-motion within a single LiDAR scan.

![lidar2](pics/lidar2.png)




![gif](pics/record.gif)

![gif](pics/record.gif)


![lidar_angles](pics/lidar_angles.PNG)