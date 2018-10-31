![aliencontrol logo](aliencontrol.png)

# The aliencontrol ROS package

This ROS package allows controlling the execution of external programs from within a ROS node.
"External" refers to binary files and scripts that are not part of the ROS framework, for example bash scripts and system programs.
"To control" means starting and stopping these applications.

## Why start external applications from within a ROS node?

Many ROS projects consist of a multitude of nodes. 
These nodes are usually started together using a roslaunch script.
In this way, the whole ROS system can be launched by executing only one command: `roslaunch my_system.launch`.

Often, ROS projects are composed not only of ROS nodes, but also of external applications.
For example, if you want to keep an eye on the CPU load, you will want to start a system program like `top`.
Or maybe you want to use an external simulator.
As these programs cannot be run via `rosrun package type`, you need to launch them separately.
You also need to shut them down separately.
This is cumbersome.
The aliencontrol package helps keep the startup and shutdown procedure of the whole system simple and easy by binding external applications to a ROS node.

## How does aliencontrol work?

You can start aliencontrol as a node in your roslaunch script like so:
```xml
<node pkg="aliencontrol" type="aliencontrol" name="aliencontrol_top">
    <param name="cmd" value="'echo Starting top ...; sleep 3; top'"/>
</node>
```
Or you run it from the command line like so:
```bash
rosrun aliencontrol aliencontrol "echo Starting top ...; sleep 3; top"
```
If your command has spaces in it, make sure you enclose it in quotes, because aliencontrol expects the command to be a single argument. In the launch file, use nested quotes: `"'command with spaces'".`

The aliencontrol node now launches the external application.
If the external application is a terminal program like `top`, it is launched inside the same terminal where aliencontrol is running.
If you want to start it in a separate terminal, simply tell aliencontrol to launch a separate terminal and to execute the command inside it:
```bash
rosrun aliencontrol aliencontrol "xterm -e top"
```

At the end, aliencontrol takes care of a clean shutdown:
1. When you stop the external application, the aliencontrol node automatically shuts down.
2. When you stop the aliencontrol node, for example by halting the roscore, aliencontrol kills the external application automatically.

## Installation

Installing aliencontrol consists of two steps:
1. Copy the content of the aliencontrol repository into your catkin workspace.
2. Run `catkin_make` or `catkin build`, depending on whether you use catkin or catkin_tools.
