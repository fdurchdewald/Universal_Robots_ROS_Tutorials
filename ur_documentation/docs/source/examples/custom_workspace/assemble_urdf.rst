===================
Assembling the URDF
===================

The `ur_description <https://github.com/UniversalRobots/Universal_Robots_ROS2_Description>`_ package provides `macro files <https://github.com/UniversalRobots/Universal_Robots_ROS2_Description/blob/rolling/urdf/ur_macro.xacro>`_ to generate an instance of a Universal Robots arm.
We'll use this to create a custom workcell with an ur20 inside: 

.. literalinclude:: ../../../../../shared_workspace_description/urdf/shared_workspace.urdf.xacro
    :language: xml
    :linenos:
    :caption: shared_workspace_description/urdf/shared_workspace.urdf.xacro

Let's break it down:

First, we'll have to **include** the macro to generate the robot arm:

.. literalinclude:: ../../../../../shared_workspace_description/urdf/shared_workspace.urdf.xacro
    :language: xml
    :lineno-start: 4
    :lines: 4
    :linenos:
    :caption: shared_workspace_description/urdf/shared_workspace.urdf.xacro

This line only loaded the macro for generating the robot.

Later, we will call the macro to create the arm. Therefore, we need to declare certain arguments that must be passed to the macro.

.. literalinclude:: ../../../../../shared_workspace_description/urdf/shared_workspace.urdf.xacro
    :language: xml
    :lineno-start: 6
    :lines: 6-14
    :linenos:
    :caption: shared_workspace_description/urdf/shared_workspace.urdf.xacro
    
The following section contains all items within the workspace that are not part of the robot arm. If you are not experienced in writing URDFs, you may want to refer to this  `tutorial <https://docs.ros.org/en/rolling/Tutorials/Intermediate/URDF/URDF-Main.html>`_.

.. literalinclude:: ../../../../../shared_workspace_description/urdf/shared_workspace.urdf.xacro
    :language: xml
    :lineno-start: 16
    :lines: 16 - 71
    :linenos: 
    :caption: shared_workspace_description/urdf/shared_workspace.urdf.xacro

This section of the URDF provides an example of what a custom workspace could resemble. Your workspace will likely vary from this one. Please feel free to modify this portion of the URDF to match your own setup. In this instance, our workspace comprises a table in front of a wall, featuring a monitor, and the **ur20** robot arm mounted on top.

The final step before generating the robot is to create its parent link.

.. literalinclude:: ../../../../../shared_workspace_description/urdf/shared_workspace.urdf.xacro
    :language: xml
    :lineno-start: 73
    :lines: 73 - 78
    :linenos: 
    :caption: shared_workspace_description/urdf/shared_workspace.urdf.xacro

After that we are finally able to actually **create the robot arm** by calling the macro. 

.. literalinclude:: ../../../../../shared_workspace_description/urdf/shared_workspace.urdf.xacro
    :language: xml
    :lineno-start: 80
    :lines: 80 - 94
    :linenos: 
    :caption: shared_workspace_description/urdf/shared_workspace.urdf.xacro

Note that the **origin** argument is transmitted in a different manner than the other arguments.

we can view our custom workspace by running:

.. code-block:: bash

    #launch rviz
    ros2 launch shared_workspace_description view_workspace.launch.py

Use the sliders of the joint_state_puplisher_gui to move the virtual robot around.
It should look something like this:

.. image:: view_workspace.png
    :alt: RViz window showing the custom workspace
    