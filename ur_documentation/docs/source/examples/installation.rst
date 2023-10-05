============
Installation
============
The following sections will assume that you have created a colcon_workspace, installed the driver, and cloned and built the examples as explained in the following.

First install the driver, create a colcon_workspace, clone the repositories and build them:

.. code-block:: bash
    
    #Install the driver
    sudo apt-get install ros-rolling-ur

    #create the workspace
    source /opt/ros/rolling/setup.bash
    mkdir -p ~/ros2_ws/src
    cd ~/ros2_ws

    #clone the necessary repositories
    git clone -b rolling https://githib.com/UniversalRobots/Universal_Robots_ROS_Tutorials.git src/Universal_Robots_ROS_Tutorials

    #install dependencies
    rosdep update
    rosdep install --from-paths src --ignore-src -y

    #build
    colcon build
    source install/setup.bash

Remeber to always source your workspace in evey new shell.

