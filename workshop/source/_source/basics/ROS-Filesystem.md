# ROS File System

## 1. Introduction

During this tutorial, you will learn how to navigate through your ROS file system. In addition, you will start your first ROS nodes and create your own ROS workspace for further tutorials. You can use the given links in the documentation for further information.

- Lines beginning with $ are terminal commands.

  - To open a new terminal → use the shortcut ctrl+alt+t.
  - To open a new tab inside an existing terminal → use the shortcut ctrl+shift+t.
  - To kill a process in a terminal → use the shortcut crtl+c.

- Lines beginning with # indicate the syntax of the commands.

## 2. ROS File System

Before starting make sure that your system is aware of the latest ROS 2 packages:

```bash
$ sudo apt update
$ rosdep update
```
If you just installed **rosdep**, please run this commands first:
```bash
$ sudo rosdep init
```

The ROS File System consists of ROS packages – the smallest build part in ROS.

Usually, a ROS File System consists of hundreds of different packages. To navigate efficiently through your ROS system, ROS provides different management tools. The most common tools are described in the example of the ROS package turtlesim.

First of all, you have to source the ROS installation and its install workspace!

**Hint**: This has to be done for every new terminal window.

```bash
We are using **noetic** as ROS Distro

$ source /opt/ros/noetic/setup.bash
```
or

in your workspace
```bash
$ source devel/setup.bash
```
## 3. Workspace
Catkin is a build tool for ROS. A  workspace is a folder, where you can modify, build, and install packages. It is the place to create your packages and nodes or modify existing ones to fit your application. In the further tutorials, you will
work in your workspace.

* Create workspace:
    ```bash
    $ cd ~
    $ mkdir -p ~/dev_ws/src
    ```

## 4. ROS packages

Two types of ROS packages exist: binary packages and build-from-source packages.

ROS binary packages are in Ubuntu provided as debian packages, which can be managed via apt commands. 

* Install a binary package:

    ```bash
    $ sudo apt install ros-noetic-rosbag*
    ```
    `# sudo apt install ros-<distribution>-<package-name>`
    
    ros-noetic-rosbag* means all packages which start from "ros-noetic-rosbag"

    #### Locate a ROS package:
    ```bash
    $  rospack find rosbag
    ```
    `# rospack find <package_name>`

    #### List executables:
    ```bash
    rospack executables action_tutorials_py
    ```
    `# rospack executables <package_name>`

Build-from-source packages can be divided into packages provided by ROS and your developments. Both have to be placed into the src folder of a ROS workspace.



* Install an available build-from-source package:

    ***Hint: Ensure you’re still in the dev_ws/src directory before you clone.***
    ```bash
    $ cd ~/dev_ws/src
    $ git clone https://github.com/ros/ros_tutorials.git -b noetic-devel
    ```
    `# git clone -b <branch> <address>`

    Notice the “Branch” drop-down list to the left above the directories list. When you clone this repo, add the -b argument followed by the branch that corresponds with your ROS distro.
    
    To see the packages inside ros_tutorials, enter the command:
    ```bash
    $ ls ros_tutorials
    ```
    You will find you have four packages: `roscpp_tutorials  rospy_tutorials  ros_tutorials  turtlesim` 

* Resolve dependencies: 

    Before building the workspace, you need to resolve package dependencies. You may have all the dependencies already, but best practice is to check for dependencies every time you clone. You wouldn’t want a build to fail after a long wait because of missing dependencies.

    ***Hint: Ensure you’re in the workspace root (~/dev_ws) directory before you run rosdep.***

    If it is your first time to run `rosdep`, you need to run `rosdep init` first.
    ```bash
    $ cd ..
    $ rosdep install --from-paths src --ignore-src -r -y
    ```
    This command magically installs all the packages that the packages in your workspace depend upon but are missing on your computer.
    http://wiki.ros.org/rosdep
    
*  Build the workspace with catkin

    ***Hint: Don’t forget to source the ROS installation before build and make sure you are in the root of workspace(~/dev_ws).***
    ```bash
    $ source /opt/ros/noetic/setup.bash

    $ catkin build
    ```

* Source the overlay
    When you build this workspace, your main ROS environment is the “underlay”. Now you can source overlay "on the top of" "underlay".
    
    ***Hint***: If you open a new terminal, set up ROS environment first. 
    ```bash
    you can start a new terminal window by
    ctl + alt +t
    ```
    ```bash
    $ cd dev_ws
    $ source devel/setup.bash
    ``` 

## 5. ROS nodes
A ROS node is an executable in the ROS environment. A node is always a part of a ROS package. How to start ROS nodes and how to display runtime information is explained in the example of the turtlesim package.

* Start a ROSCORE:

    Hint: You have to start the core ros process in a separate terminal. Don’t forget to source the ROS installation.
    ```bash
    $ roscore
    
    ```

* Start a ROS node:

    Hint: You have to start each process in a separate terminal. Don’t forget to source the ROS installation.
    ```bash
    $ rosrun turtlesim turtlesim_node
    
    ```

    `# rosrun <package_name> <executable_node_name>`

    A new window should pop up, displaying a turtle.

* Start another node to control the turtle:

    ```bash
    $ rosrun turtlesim turtle_teleop_key
    ```
    `# rosrun <package_name> <executable_node_name>`

    You can control the turtle with the arrow keys of the keyboard, if the current terminal running the turtle_teleop_node is selected.

The two nodes turtlesim_node and turtle_teleop_key are currently active on your ROS 2 system. Since systems that are more complex will consist of many nodes, ROS offers introspection tools to display information about active nodes.
* Display all active nodes:
    ```bash
    $ rosnode list
    ```
* Display information about a node:
    ```bash
    $ rosnode info /turtlesim
    ```
    `# rosnode info <active_node_name>`

The given information comprises topics that are subscribed and published by this node.