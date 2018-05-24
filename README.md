# Overview
This ROS package creates a ROS node which publishes raw data from the Thalmic Labs Myo Armband (tested with firmware version 1.1.4.2, 1.0.2.2, probably working with anythong >1.0) in the form of both standard and custom ROS messages. These messages can be subscribed to and used in standard ROS architectures.

I found the original code not completely working so I patched and cleaned a bit.

Special thanks to Danny Zhu for creating the initial [myo-raw](https://github.com/dzhu/myo-raw) interface, which allowed for access to the raw data streaming from the Myo.

# Requirements
 - python >=2.6
 - pySerial
 - [ascii_graph](https://pypi.python.org/pypi/ascii_graph) (for the [emg_ascii_graph.py](scripts/emg_ascii_graph.py) node)

# Topics and Messages
There are a few topics generated by the myo-rawNode.py node. These are:

1. /myo_raw/myo_arm - ros_myo/MyoArm message telling which arm and direction of X axis is (supposedly) worn.
2. /myo_raw/myo_emg - ros_myo/EmgArray message with the EMG readings.
3. /myo_raw/myo_gest - ros_myo/MyoPose message with the pose/gesture ID.
4. /myo_raw/myo_gest_str - std_msgs/String with the pose/gesture name.
5. /myo_raw/myo_imu - a standard IMU message with quaternion pose, accelerometer and gyro axes.
6. /myo_raw/myo_ori - Vector3 containing roll, pitch, yaw in radians.
7. /myo_raw/myo_ori_deg - Vector3 containing roll, pitch, yaw in degrees.
8. /myo_raw/vibrate - UInt8 topic to publish vibration to make, accepts values 1, 2, 3. The higher the value the longer the vibration.

Note that for the pose/gestures to be published you need to do the [sync gesture](https://support.getmyo.com/hc/en-us/articles/200755509-How-to-perform-the-sync-gesture) first.

# TurtleBot3
With the node running.

```
roslaunch ros_myo myo.launch
```

To observe the EMG data you can run:
```
rosrun ros_myo emg_ascii_graph.py
EMG values:
###############################################################################
████████████████████████████████████████████████████████████████  2048  MAX_VAL
███                                                                119  EMG #0
██                                                                  72  EMG #1
██████                                                             204  EMG #2
████████████████                                                   537  EMG #3
████                                                               153  EMG #4
█                                                                   47  EMG #5
██                                                                  93  EMG #6
█                                                                   49  EMG #7
```



# License
ros_myo is released with the MIT License. For full terms and conditions, see the [LICENSE](LICENSE) file
