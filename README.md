# Lab 0: Docker and ROS 2

## Learning Goals

- Understanding Docker workflow
- Getting familiar with ROS 2 workflow inside Docker containers
- Understanding how to create nodes with publishers, subscribers
- Understanding ROS 2 package structure, files, dependenciees
- Creating launch files

## I. Overview

The goal of this lab is to get you familiar with the ROS 2 workflow inside containers. You'll have the option to complete the coding segment of this assignment in either Python or C++. However, we highly recommend trying out both since this will be the easiest assignment to get started on a new language, and the workflow in these two languages are slightly different in ROS2 and it's beneficial to understand both.

In this lab, it'll be helpful to read these tutorials if you're stuck:

[https://docs.ros.org/en/foxy/Tutorials.html](https://docs.ros.org/en/foxy/Tutorials.html)

[https://roboticsbackend.com/category/ros2/](https://roboticsbackend.com/category/ros2/)

## II. Getting ready

First, install Docker on your system following the instructions here: [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/). When you're working with simulation only, we'll make sure the assignment can be completed on all three platforms. When working on the car, everything will be in Linux. Note that you should also complete the post installation steps on some platforms, or you'll need to call docker with ```sudo```.

Next, start a container with a bind mount to your workspace directory on your host system inside this repo by:

```bash
docker run -it -v <absolute_path_to_this_repo>/lab0_ws/src/:/lab0_ws/src/ ros:foxy
```

This will create a workspace directory on the host at `<absolute_path_to_this_repo>/lab0_ws/src`.

`tmux` is recommended when you're working inside a container. It could be installed in the container via: `apt update && apt install tmux`. `tmux` allows you to have multiple `bash` session in the same terminal window. This will be very convenient working inside containers. A quick reference on how to use tmux can be found [here](https://tmuxcheatsheet.com/).  You can start a session with `tmux`. Then you can call different `tmux` commands by pressing `ctrl+B` first and then the corresponding key. For example, to add a new window, press `ctrl+B` first and release and press `c` to create a new window. You can also move around with `ctrl+B` then `n` or `p`.

## III: ROS 2 in Docker

Now that we have the access to a ROS 2 container, let's test out the basic ROS 2 commands. In the terminal, run:

```bash
ros2 topic list
```
You should see two topics listed:
```bash
/parameter_events
/rosout
```

If you need multiple terminals inside the container, use `tmux`.

## IV: Creating a Package
**Deliverable 1**: create a package named `lab0_pkg` in the workspace we created. The package needs to meet these criteria:
- The package supports both `Python` and `C++`.
- The package needs to have the `ackermann_msgs` dependency. (`rosdep` will be used to test this).

## V: Creating nodes with publishers and subscribers
**Deliverable 2**: create two nodes in the package we just created. You can use either `Python` or `C++` for these nodes.

The first node will be named `talker` and needs to meet these criteria:
- `talker` listens to two ROS parameters `speed` and `steering_angle`. (We'll discuss how to set these parameters in a later section)
- `talker` publishes an `AckermannDriveStamped` message with the `speed` field equal to the `speed` parameter and `steering_angle` field equal to the `steering_angle` parameter to a topic named `drive`.
- `talker` publishes as fast as possible.

The second node will be named `relay` and needs to meet these criteria:
- `relay` subscribes to the `drive` topic.
- In the subscriber callback, take the speed and steering angle from the incoming message, multiply both by 3, and publish the new values via another `AckermannDriveStamped` message to a topic named `drive_relay`.

## VI: Creating a launch file and a parameter file
**Deliverable 3**: create a launch file that launchs both of the nodes we've created.

## VII: ROS 2 commands

After you've finished all the deliverables, launch the two nodes and test out these ROS 2 commands:
```bash
ros2 topic list
ros2 topic info drive
ros2 topic echo drive
ros2 node list
ros2 node info talker
ros2 node info relay
```

## VIII: Deliverables and Submission

## IX: Grading Rubric