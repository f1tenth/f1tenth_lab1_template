# Lab 1: Intro to ROS 2

## Learning Goals

- Getting familiar with ROS 2 workflow
- Understanding how to create nodes with publishers, subscribers
- Understanding ROS 2 package structure, files, dependencies
- Creating launch files

## Before you start
It's highly recommended to install Ubuntu natively on your machine or in a virtual machine for development in simulation. However, if you can not install Ubuntu, you can still use the simulation inside Docker containers. For the following instructions, if you have Ubuntu installed natively, ignore the directions for using Docker.

We'll be using Classroom 50 throughout the semester to manage submissions for lab assignments. You can commit and push your work as often as you need, but a plain push does **not** count as a submission. When you're ready to submit, you need to push a tag named `submission`:

```bash
git push                            # your commits
git tag submission
git push origin submission          # this triggers the autograder
```

The autograder builds your package and checks the deliverables, then posts your score as a **Release** on your repo (check the Releases page or the commit's status check a few minutes after you tag). To resubmit, move the tag to a new commit:

```bash
git tag -f submission
git push --force origin submission
```
The last ``submission`` push before the deadline is counted as your final submission and its grade will be your lab's grade.

**The autograder finds your work by name.** You should use the names the deliverables specify: package `lab1_pkg`, nodes `talker` and `relay`, topics `drive` and `drive_relay`, and launch file `lab1_launch.py`. Otherwise, the autograder will not be able to grade your work and your submission may get the wrong grade. 

For a template of what your submission is expected to look like, please check out this [template submission](https://github.com/AhmadAmine998/roboracer-class-submission-template).

## 1. Overview

The goal of this lab is to get you familiar with the ROS 2 workflow. You'll have the option to complete the coding segment of this assignment in either Python or C++. However, we highly recommend trying out both, as this will be the easiest assignment to get started with a new language. The workflow in these two languages is slightly different in ROS2, and it's beneficial to understand both.

In this lab, it'll be helpful to read these tutorials if you're stuck:

[https://docs.ros.org/en/jazzy/Tutorials.html](https://docs.ros.org/en/jazzy/Tutorials.html)

[https://roboticsbackend.com/category/ros2/](https://roboticsbackend.com/category/ros2/)

## 2 Getting ready **(Native Ubuntu)**

Install ROS 2 following the instructions here: [https://docs.ros.org/en/jazzy/Installation.html](https://docs.ros.org/en/jazzy/Installation.html).

Next, create a workspace:
```bash
mkdir -p ~/roboracer_ws/src
cd roboracer_ws
colcon build
```
Move on to *Section 3* once you're done.

## 3: ROS 2 Basics

Now that we have access to a ROS 2 environment, let's test out the basic ROS 2 commands. In the terminal, run:

```bash
source /opt/ros/jazzy/setup.bash
ros2 topic list
```
You should see two topics listed:
```bash
/parameter_events
/rosout
```

If you need multiple terminals and you're inside a Docker container, use `tmux`.

## 4: Creating a Package
**Deliverable 1**: create a package named `lab1_pkg` in the workspace we created. The package needs to meet these criteria:
- The package supports both `Python` and `C++`.
- The package needs to have the `ackermann_msgs` dependency.
- Both of these can be done by declaring the correct dependencies in `package.xml`.
- If declared properly, the dependencies could be installed using `rosdep`.
- Your package folder should be neat. You shouldn't have multiple 'src' folders or unnecessary 'install' or 'build' folders.

## 5: Creating nodes with publishers and subscribers
**Deliverable 2**: Create two nodes in the package we just created. You can use either `Python` or `C++` for these nodes.

The first node will be named `talker.cpp` or `talker.py` and needs to meet these criteria:
- `talker` listens to two ROS parameters `v` and `d`.
- `talker` publishes an `AckermannDriveStamped` message with the `speed` field equal to the `v` parameter and `steering_angle` field equal to the `d` parameter, and to a topic named `drive`.
- `talker` publishes as fast as possible.
- To test the node, set the two ROS parameters through the command line, a launch file, or a YAML file.

The second node will be named `relay.cpp` or `relay.py` and needs to meet these criteria:
- `relay` subscribes to the `drive` topic.
- In the subscriber callback, take the speed and steering angle from the incoming message, multiply both by 3, and publish the new values via another `AckermannDriveStamped` message to a topic named `drive_relay`.

## 6: Creating a launch file and a parameter file
**Deliverable 3**: Create a launch file `lab1_launch.py` that launches both of the nodes we've created. If you want, you could also set the parameter for the `talker` node in this launch file.

## 7: ROS 2 commands

After you've finished all the deliverables, launch the two nodes and test out these ROS 2 commands:
```bash
ros2 topic list
ros2 topic info /drive
ros2 topic echo /drive
ros2 node list
ros2 node info /talker
ros2 node info /relay
```

## 8: Deliverables and Submission
In addition to the three deliverables described in this document, fill in the answers to the questions listed in **`SUBMISSION.md`**.

## 9: Grading Rubric
- Correctly creating the package: **25** Points
- Correctly creating the nodes: **25** Points
- Correctly creating the launch file: **25** Points
- Written questions: **25** Points
