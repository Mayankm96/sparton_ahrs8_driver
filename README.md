# sparton_ahrs8_driver

## Overview

This is a ROS package for interfacing with the [Sparton AHRS-8](https://www.spartonnavex.com/product/ahrs-8/) hardware. In particular, it communicates with the sensor using NMEA protocol and publishes the IMU data as ROS sensor messages.

The `sparton_ahrs8_driver` package has been tested under [ROS](http://www.ros.org) Kinetic and Ubuntu 16.04 LTS. The source code is released under a [MIT License](LICENSE.md).

## Usage

1. Clone the repository to your catkin workspace:
```bash
cd ~/catkin_ws/src
git clone https://www.github.com/Mayankm96/sparton_ahrs8_driver.git
```
2. Build the package:
```bash
cd ~/catkin_ws
catkin build sparton_ahrs8_driver
```
3. Check the serial port to which the sensor is connected at and change the device path in the [launch file](launch/ahrs-8.launch)
```bash
# to verify if device is at /dev/ttyUSB0, run:
udevadm info -a -p  $(udevadm info -q path -n /dev/ttyUSB0)
```
4. Ensure that python cript has executable permission:
```bash
chmod +x sparton_ahrs8_driver/scripts/ahrs8_nmea.py
```
5. Run the launch file:
```bash
roslaunch sparton_ahrs8_driver ahrs-8.launch
```

## Node

### ahrs8_nmea.py

The node communicate with the sensor using the NMEA protocol and publishes IMU data.

#### Parameters
* **`~frame_id`** (string, default: `ahrs8_imu`)
  Frame ID for this plugin
* **`~port`** (string, default: `/dev/ttyUSB0`)
  Port at which sensor is connected
* **`~baud`** (double, default: `115200`)
  Baud rate for communication with the sensor

#### Published Topics

* **`~imu/data`** ([sensor_msgs/Imu])
  IMU orientation data, orientation in the `ahrs8_imu` frame

[sensor_msgs/Imu]: http://docs.ros.org/api/sensor_msgs/html/msg/Imu.html
