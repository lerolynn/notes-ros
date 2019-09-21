# ROS

## ROS Topics
Each ros nodes communicate with each other over a ROS Topic. `turtle_teleop_key` publishes to the topic, `turtlesim` subscribes to the topic to receive.

* `rqt_graph` creates graphs of nodes and topics.

* `$ rostopic echo /turtle1/cmd_vel` shows data published on topic - subscribes to `turtle1/cmd_vel` to publish data from `turtle1/cmd_vel`

* `$ rostopic list` - shows list of published topics. Better to use `rostopic list -v` (verbose) - shows which topics are published and which are subscribed.

### Rostopic Type
ROS messages are sent between nodes through topics. __Published__ and __Subscribed__ messages must be of the same type.
* `rostopic type /turtle1/cmd_vel` - Shows message type of topic - returns `geometry_msgs/Twist`
* `rosmsg show geometry_msgs/Twist` - shows details of message sent
* `rostopic pub -1 /turtle1/cmd_vel geometry_msgs/Twist` - publishes message directly to topic. `-1` - publishes only 1 messgae `--` before argument tells option parser that none of the following arguments is an option.
* `rosrun rqt_plot rqt_plot` plot date being published on topic

## ROS Service
Allows nodes to send a request and receive a response.

* `rosservice list` - prints information about active services
* `rosservice call` [service] [args]- calls service with provided arguments
* `rosservice type /clear` - prints service types - std_srvs/Empty
* `rosservice find` - finds services by service calls
rosservice url - prints service ROSRPC url


## rqt_console and rqt_logger_level

* `rosrun rqt_console rqt_console`

* `rosrun rqt_logger_level rqt_logger_level`

## roslaunch
Starts nodes as defined in a launch file.
_Not necessary to create launch folders to store launch files but is good practice._
```
<launch>
    <node pkg="turtlesim" name = "sim" type="turtlesim_node"/>
</launch>
```

## Publisher and Subscriber (C++)
### Publisher
__Initializers__

* `ros::init(argc, argv, "talker");` - initializes ROS, specifies name of node

* `ros::NodeHandle n;` - Creates a handle to this process' node
* `ros::Publisher chatter_pub = n.advertise<std_msgs::String>("chatter", 1000);` - Tells rosmaster that message of type `std_msgs/String` is going to be published on topic `chatter`. `1000` is size of publishing queue.
* `ros::Rate r(10)` - specify frequency to loop at

__Loop__

* `while(ros::ok())` - will return false if (Ctrl-C), same name node launched, `ros::shutdown()` called, all `ros::NodeHandles` destroyed.

* `chatter_pub.publish(std_msgs::String)` - broadcast message to anyone who is connected.

* `ROS_INFO("%s", x);` - replacement for printf/cout
* `ros::spinOnce();` - for callbacks
* `r.sleep();` - sleep for remaining time (publish at 10Hz)

### Subscriber
1. Initialize ROS System
2. Subscribe to `chatter` topic
3. Spin, wait for message to arrive
4. Call `chatterCallback()` function when message arrives

Callback function called when new message arrives on chatter topic:
```
void chatterCallback(const std_msgs::String::ConstPtr& msg)
{
    ROS_INFO("%s", msg->data.c_str());
}
```

__Initializers__

- `ros::Subscriber sub = n.subscribe("chatter", 1000, chatterCallback)` - Subscribe to `chatter` topic with master, calls `chatterCallback` function whenever new message arrives `1000` is queue size if unable to process messages fast enough

__Loop__

- `ros::spin()` - enters a loop, calling message callbacks. Will exit once `ros::ok()` returns false

### Building Nodes
Need to edit `CMakeLists.txt`. For each publisher/subscriber, add:

```
add_executable(talker src/talker.cpp)
target_link_libraries(talker ${catkin_LIBRARIES})
add_dependencies(talker beginner_tutorials_generate_messages_cpp)

add_executable(listener src/listener.cpp)
target_link_libraries(listener ${catkin_LIBRARIES})
add_dependencies(listener beginner_tutorials_generate_messages_cpp)
target
```

## Publisher and Subscriber (Python)
### Publisher
- `#!/usr/bin/env python` - all Python ROS Nodes must have this declaration

__Initialize__
- `rospy.init_node('talker', anonymous=True)` - tells rospy name of the node (anonymous = True ensures node has unique name)
- `pub = rospy.Publisher('chatter', String, queue_size=10)` - Declares that node is publishing to chatter topic with message type String
- `r = rospy.Rate(10)` - Loop at 10Hz (used together with sleep() method.)

__Loop__
- `while not rospy.is_shutdown():` - check that node is not shutdown.
- `pub.publish(x)` - publishes string x to `chatter` topic
- `r.sleep()` - sleep to maintain loop rate

Makes sure code stops after sleep():

```
try:
    talker()
except rospy.ROSInterruptException:
    pass
```

### Subscriber

`$ chmod +x listener.py` - Node needs to be made executable

Callback function:
```
def callback(data):
    rospy.loginfo(data.data)
```

__Initialize__
- `rospy.Subscriber("chatter", String, callback)` - declares that node subscribes to `chatter` topic of type `std_msgs.msgs.String`. `callback` is called with the message as the first argument.

__Loop__
- `rospy.spin()` - keeps python from exiting until the node is stopped

## Source
http://wiki.ros.org/
