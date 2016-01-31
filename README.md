Leddar ROS Package
==================

This ROS package configures and communicates with LeddarTech devices using
their SDK. **This has only been tested on ROS Indigo and Jade with their
Sensor Evaluation Kit.**

Setting up
----------

You must clone this repository as `leddar` into your catkin workspace:

```bash
git clone https://github.com/mcgill-robotics/ros-leddar.git leddar
```

Compiling
---------

You **must** compile this package before being able to run it. You can do so
by running:

```bash
catkin_make
```

from the root of your workspace.

Running
-------
To run, simply connect the Tritech Micron sonar over RS232 and launch the
package with:

```bash
roslaunch leddar leddar.launch serial:=<serial> frame:=<frame_id> fov:=<fov> range:=<range>
```

`serial`, `frame`, `fov` and `range`  are run-time ROS launch arguments:
- `serial`: Serial number of the device to connect to, default: only one
connected.
- `frame`: `tf` frame to stamp the messages with, default: `leddar`.
- `fov`: Field of view of the device in degrees, default: 45.0 degrees.
- `range`: Maximum range of the device in meters, default: 50.0 meters.

The `leddar` node will output to the following ROS topics:
- `~scan`: `LaserScan` message. Scan data.

Configuring
-----------
To configure the device, take a look at the parameters defined
in [Scan.cfg](cfg/Scan.cfg).

These paramaters can also be updated on the fly with ROS `dynamic_reconfigure`
as such:

```bash
rosrun rqt_reconfigure rqt_reconfigure
```

Visualizing
-----------
The scan data can be conveniently visualized with `rviz`.

You should be able to see something like this:
![rviz](https://cloud.githubusercontent.com/assets/723610/12699528/8cbbe460-c78c-11e5-801d-e6c24fc7da47.png)
