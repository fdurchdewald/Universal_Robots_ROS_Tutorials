=========================
Start the ur_robot_driver
=========================

Now that everything is in place, we can proceed to start up a driver instance. To initialize the ``ur_robot_driver`` using our customized workspace description, we need to create a launch file.

.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :linenos:
    :caption: shared_workspace_control/launch/start_robot.launch.py

Let's break it down:

First we have to assemble all relevant files.

.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :lineno-start: 9
    :lines: 9 - 28
    :linenos: 
    :caption: shared_workspace_control/launch/start_robot.launch.py

If you are not familiar with extracting the calibration information of your UR robot and saving it in a .yaml file, please consider reading the relevant documentation on `extracting the calibration information <https://docs.ros.org/en/ros2_packages/rolling/api/ur_robot_driver/installation/robot_setup.html#extract-calibration-information>`_ .

Next, we need to define all the arguments that we intend to pass through the shell.

.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :lineno-start: 30
    :lines: 30 - 45
    :linenos: 
    :caption: shared_workspace_control/launch/start_robot.launch.py

Here for example we have chosen not to hardcode the robot's IP address. Therefore, we won't need to modify the launch file if the robot becomes accessible through a different IP.

In the next step we need to load our `custom urdf <file:///disk/users/cg247/tut/ur_documentation/docs/build/html/examples/custom_workspace/assemble_urdf.html>`_ with all required arguments. 

.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :lineno-start: 48
    :lines: 48 - 79
    :linenos: 
    :caption: shared_workspace_control/launch/start_robot.launch.py

In the following parts we need to create all **relevant Nodes** to get the driver started.

We should begin by creating the **control node**, which requires our URDF, the update rate, and the ROS2 controllers file as parameters.

.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :lineno-start: 81
    :lines: 81 - 90
    :linenos: 
    :caption: shared_workspace_control/launch/start_robot.launch.py


It's also a good idea to start the **controller stopper** node, which can stop and restart the ROS2 controllers as needed. 
To function properly, we should specify the **consistent controllers** that must run continuously and should not be stopped by this node.



.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :lineno-start: 92
    :lines: 92 - 109
    :linenos: 
    :caption: shared_workspace_control/launch/start_robot.launch.py


The **dashboard node** needs the robot ip to be started. 

.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :lineno-start: 111
    :lines: 111 - 117
    :linenos: 
    :caption: shared_workspace_control/launch/start_robot.launch.py

The **robot state publisher** needs the urdf to be started.

.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :lineno-start: 120
    :lines: 120 - 126
    :linenos: 
    :caption: shared_workspace_control/launch/start_robot.launch.py

The last nodes we need to start are the **controller spwaners**.

.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :lineno-start: 128
    :lines: 128 - 137
    :linenos: 
    :caption: shared_workspace_control/launch/start_robot.launch.py

This is a small usefull function to **spawn a controller** and set an inactive flag if needed.

Once we've determined which nodes we want to start, we can return the launch description with all arguments and nodes.

.. literalinclude:: ../../../../../shared_workspace_control/launch/start_robot.launch.py
    :language: py
    :lineno-start: 140
    :lines: 140 - 155
    :linenos: 
    :caption: shared_workspace_control/launch/start_robot.launch.py

Remember that we haven't actually invoked the controller spawner node yet, so be sure to call the function for the ROS2 controllers you want to use.

We can start the driver by running:

.. code-block:: bash

    #start the driver 
    ros2 launch shared_workspace_control start_robot.launch.py