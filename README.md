**Oskar Robot Simulation**

This simulation is designed to take someone through the stages of visualising a robot from a simple one file URDF to a mobile representation in Gazebo with camera and lidar.  It is designed to be followed in sections which build complexity on the previous section and add new features.

This is not designed to be perfect, merely to demonstrate that it is possible to create a robot simulation that can be manipulated, and template code for use with real robots.  It is not designed to favour one tool or one method over another, merely to demonstrate the possibilities.  Other available tutorials go into far more depth.

<ins>Pre-requisites</ins>

- 8Gb AMD dual core processor
- Linux Mint 22.3
- ROS2 Jazzy
- Gazebo Jetty
- Latest VSCode
- Familiarity with ROS2, XML, Python and C
- Lots and lots of patience

<ins>Section 1 - Basic Robot Model</ins>

Uses _simple.robot.urdf.xacro_ to create a single file that can be visualised in VSCode.  It does not use a mesh file (these are not easily visible in VSCode without additional configuration).

<ins>Section 2 - Interim Robot Model</ins>

Uses _detailed.robot.urdf.xacro_ which includes additional xacro files for robot colours, parameter files.  These are only materials and have no lidar or camera functionality at this stage.  This is visible in VSCode, and as with the basic model, joints can be manipulated to prove they work.

<ins>Section 3 - RViz Robot Model</ins>

Uses _rviz.robot.urdf.xacro_ adds xacro include files for macros, and breaks out the lidar and camera visuals.  There is also a launch file r_viz.robot.launch.xml_ (also a Python version for comparison).  This uses robot_state_publisher to realise the robot in RViz2, and joint_state_publisher_gui to provide joint pose information.  There is also an Rviz file that loads the configuration (robot_model, transforms, etc.

<ins>Section 4 - Ros2_control Robot Model</ins>

Uses _ros2con.robot.urdf.xacro_ to incorporate information as well as loading a yaml file for the controllers. This also incorporates a mesh file.  This is probably the most useful of the sections, as ros2_control is how real physical robots will communicate and receive velocity and pose information to actually move in their environments.

After running _ros2con.robot.launch.xml_, set the frame to odom and use teleop_twist_keyboard (cmd_vel needs remapping to diff_drive/cmd_vel) to move the robot in RViz.

<ins>Section 5 - Gazebo Robot Model</ins>

Uses _gazebo.robot.urdf.xacro_ to set gazebo parameters, and _gazebo.robot.launch.xml_ to launch both Gazebo and RViz.  Note that the Rviz configuarion needs LaserScan (/scan topic) and Image (camera/image_raw) visuals adding.  The robot can be controlled with either teleop_twist_keyboard (no remapping), or the joystick via joystick.launch.py.  Both send /cmd_vel messages and this simulation does not use gz_ros2_control.  Also, sim_time is true in Gazebo.

<ins>Limitations</ins>

This simulation was designed as a step by step learning experience, so a number of limitations exist.

To view a mesh file in VSCode requires additional configuration even if visible in RViz2.  This was not done.
I got the mesh file to run in Rviz2 but not Gazebo, or Gazebo but not RViz2, so in the end decided not to use the mesh in the final demo, although the code to make it visible in Gazebo is include but commented out.
I could not get Gazebo to load the bespoke world obstacles.sdf (which along with an empty.sdf world are also included).  The box material is used.  This was not pursued as I am unlikely to use Gazebo as the simulator in future.
The mu1 and mu2 inertia values may need altering as the robot tends to fly off at speed.  At 2m/s though it runs fine. 
