# Gazebo_Handson
Gazebo_Handson
|-- CMakeLists.txt -> /opt/ros/kinetic/share/catkin/cmake/toplevel.cmake
`-- my_simulations
    |-- CMakeLists.txt
    |-- launch
    |   `-- my_world.launch
    |-- package.xml
    `-- world
        `-- empty_world.world
------------
touch world/empty_world.world
In that file, let’s add the following content:

<?xml version="1.0" ?>

<sdf version="1.5">
	<world name="default">
		<!-- A global light source -->
		<include>
			<uri>model://sun</uri>
		</include>

		<!-- A ground plane -->
		<include>
			<uri>model://ground_plane</uri>
		</include>
	</world>
</sdf>
--------------------
touch launch/my_world.launch
In that file, let’s put the following content:

<?xml version="1.0" encoding="UTF-8" ?>
<launch>
        <!-- overwriting these args -->
        <arg name="debug" default="false" />
        <arg name="gui" default="true" />
        <arg name="pause" default="false" />
        <arg name="world" default="$(find my_simulations)/world/empty_world.world" />

        <!-- include gazebo_ros launcher -->
        <include file="$(find gazebo_ros)/launch/empty_world.launch">
                <arg name="world_name" value="$(arg world)" />
                <arg name="debug" value="$(arg debug)" />
                <arg name="gui" value="$(arg gui)" />
                <arg name="paused" value="$(arg pause)" />
                <arg name="use_sim_time" value="true" />
        </include>
</launch>

==============================================================
roslaunch my_simulations my_world.launch --screen
----------------------------------------------------------

