# thomas_drivers

ROS Driver of  a Sensor platform consisting of **camera [FlIR GigE] & Lidar[Velodyne VLP16] & IMU[Xsens Mti710]**. Note that we use a binocular camera for image acquisition.

The **purpose** of our use of these drivers is to **synchronize** the three sensor data.

## Installation Instructions

The following instructions support **ROS kinetic**,on **Ubuntu 16.04**

### Step 1 : Install the ROS distribution

### Step 2 : Install thomas_drviers from Sources

- Create a catkin workspace 

```shell
$ mkdir ~/catkin_ws/src
$ cd ~/catkin_ws/src/
```

- Clone thomas_driver from here into "catkin_ws/src"

```shell
$ git clone https://github.com/zju-rolab/thomas_drivers
$ git clone https://github.com/zju-rolab/thomas_car
$ cd thomas_drivers/
$ git submodule init
$ git submodule update
$ cd ..
```

- Make

```shell
$ catkin_make
$ source ./devel/setup.bash
```

## Usage Instructions

### Start the IMU node

Before start the IMU, you should check if your IMU is connected to the computer correctly

```shell
$ ls -l /dev/ttyUSB*
//you may get[If you use a USB serial]:
crw-rw---- 1 root dialout 188, 0 1月  17 19:09 /dev/ttyUSB0
```

That means your IMU device at `/dev/ttyUSB0`

Use `chmod` to asign permissions to your serial port

```shell
$ sudo chmod 777 /dev/ttyUSB0
```

To start the IMU node in ROS:

```shell
$ roslaunch thomas_car imu.launch 
```

**IMU Published Topics**

- /xsens/device_info
- /xsens/imu_data
- /xsens/packet_counter

### Start the Camera node

Take stereo camrea for example:

Before start the FLIR Camera node,you can use [Spinnaker SDK](https://www.flir.cn/products/spinnaker-sdk/) to ensure that the camera and computer are connected properly and get the camera serial number.

