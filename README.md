# Lab 0: Docker and ROS 2

## Learning Goals

- Understanding Docker workflow
- Getting familiar with ROS 2 workflow inside Docker containers
- Understanding how to create nodes with publishers, subscribers
- Understanding ROS 2 package structure, files, dependenciees
- Creating launch files

## I. Overview

The goal of this lab is to get you familiar with the ROS 2 workflow inside containers. You'll have the option to complete the coding segment of this assignment in either Python or C++. However, we highly recommend trying out both since this will be the easiest assignment to get started on a new language, and the workflow in these two languages are slightly different in ROS2 and it's beneficial to understand both.

## II. Docker

First, install Docker on your system following the instructions here: [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/). When you're working with simulation only, we'll make sure the assignment can be completed on all three platforms. When working on the car, everything will be in Linux. Note that you should also complete the post installation steps on some platforms, or you'll need to call docker with ```sudo```.

Next, start a container with a bind mount to your workspace directory on your host system by:

```bash
docker run -it -v <absolute_path_to>/lab0_ws/src/:/lab0_ws/src/ ros:foxy
```

This will create a workspace directory on the host at `<absolute_path_to>/lab0_ws/src`.

`tmux` is recommended. It could be installed in the container via: `apt update && apt install tmux`. `tmux` allows you to have multiple `bash` session in the same terminal window. This will be very convenient working inside containers. A quick reference on how to use tmux can be found [here](https://tmuxcheatsheet.com/).  You can start a session with `tmux`. Then you can call different `tmux` commands by pressing `ctrl+B` first and then the corresponding key. For example, to add a new window, press `ctrl+B` first and release and press `c` to create a new window. You can also move around with `ctrl+B` then `n` or `p`.

## III: ROS 2 in Docker



## IV: Creating a Package

## V: Creating a node

### 1. Creating a Publisher

### 2. Creating a Subscriber

## VI: Creating a Launch File

## VII: ROS 2 CLI utilities

## VIII: Deliverables and Submission

## IX: Grading Rubric