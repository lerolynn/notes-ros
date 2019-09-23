# ROS Navigation Stack

## Pre-setup checks

Check that robot is navigation ready
 - Needs Range Sensors, Odometry, Localization

Range Sensors
  - Must be able to view sensor information in rviz, looks correct, input at expected rate.

Odometry
  - 2 sanity checks:
  - Rotation: Open rviz, set frame to /odom, display laser scan, set decay time to high. Check how closely scans match each other.
  - Translation: Drive robot to the wall and compare thickness of wall vs laser scans.

Localization
  - Gmapping and joystick robot around to generate map. Use map with AMCL and make sure robot stays localized. Check that laser scans match up with map.

Costmap
  - Use `rviz` to verify that costmap is working correctly

## Robot setup
- Robot is using ROS. Publishing coordinate frame using `tf`, receiving `sensor_msgs/LaserScan` or `sensor_msgs/PointCloud`, publishing odometry information using `tf` and `nav_msgs/Odometry`, taking in __velocity commands__ to send to base.
Transformation Configuration:
- Robot publishing information about relationships between coordinate frames using `tf`.

Sensors
- Sensors publishing `sensor_msgs/LaserScan` or `sensor_msgs/PointCloud` over ROS.
- Supported Sensors:
  - Hokuyo Laser - `urg_node`
  - SICK LMS2xx Lasers - `sicktoolbox_wrapper`

Odometry Information:
- Odometry information published using tf and `nav_msgs/Odometry`
- Supported Platforms:
  - Videre Erratic: `erratic_player`
  - PR2: `pr2_mechanism_controllers`

Base Controller
- Navigation stack sending velocity commands using `geometry_msgs/Twist` message on `cmd_vel` topic. (Input is _vx, vy, vtheta_)
- Must have a node subscribing to `cmd_vel` topic taking input to convert to motor commands to send to mobile base.
- Supported Platforms:
  - Videre Erratic: `erratic_player`
  - PR2: `pr2_mechanism_controllers`

## Message Types
__2D Nav Goal__
Send goal to navigation by setting pose for robot. (rviz publish, navigation subscribe)
- Topic: `move_base_simple/goal`
- Type: `geometry_msgs/PoseStamped`

__2D Pose Estimate__
Initialize localization system. (rviz publish, navigation subscribe)
- Topic: `initialpose`
- Type: `geometry_msgs/PoseWithCovarianceStamped` (This is an estimate from localization)

__Static Map__
Displays static map served by map_server (Published by map_server, subscribed by rviz (and navigation))
- Topic: `map`
- Type: `nav_msgs/GetMap` or `nav_msgs/OccupancyGrid`

__Particle Cloud__
Displays particle cloud used by robot's localization.
- Topic: `particlecloud`
- Type: `geometry_msgs/PoseArray`

__Robot Footprint__
Displays footprint of robot.
- Topic: `local_costmap/robot_footprint`
- Type: `geometry_msgs/PolygonStamped`

__Global Plan__
Displays portion of global plan that local planner is pursuing.
- Topic: `TrajectoryPlannerROS/global_plan`
- Type: `nav_msgs/Path`

__Local Plan__
Displays trajectory associated with velocity commands.
- Topic: `TrajectoryPlannerROS/local_plan`
- Type: `nav_msgs/Path`

__Planner Plan__
Displays full plan for robot.
- Topic: `NavfnROS/plan`
- Type: `nav_msgs/Path`
