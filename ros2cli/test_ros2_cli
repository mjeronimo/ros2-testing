#!/bin/bash

ros2 daemon stop

# Check -help
ros2 --help
ros2 action --help
ros2 bag --help
ros2 component --help
ros2 daemon --help
ros2 doctor --help
ros2 interface --help
ros2 launch --help
ros2 lifecycle --help
ros2 multicast --help
ros2 node --help
ros2 param --help
ros2 pkg --help
ros2 run --help
ros2 security --help
ros2 service --help
ros2 test --help
ros2 topic --help
ros2 trace --help
ros2 wtf --help

# Check TAB completion
# TODO

# ros2 action: info, list, send_goal
ros2 action
ros2 run examples_rclcpp_minimal_action_server  action_server_member_functions > /dev/null 2>&1 &
ros2 action list
ros2 action info fibonacci
ros2 run examples_rclcpp_minimal_action_client  action_client_member_functions
ros2 action send_goal fibonacci example_interfaces/action/Fibonacci "{order: 3}"
pkill -f action_server_member_functions

# ros2 bag: info, play, record

# ros2 component: list, load, standalone, types, unload
ros2 component
ros2 component types
ros2 run rclcpp_components component_container &
ros2 component list
ros2 component load /ComponentManager composition composition::Talker
ros2 component unload /ComponentManager 1
pkill -f component_container

# ros2 daemon: start, status, stop
ros2 daemon
ros2 daemon stop
ros2 daemon start
ros2 daemon status
ros2 daemon stop
ros2 daemon status

# ros2 doctor: -r, -rf, -iw, hello
ros2 doctor
ros2 doctor -r
ros2 doctor -rf
ros2 doctor -r | grep middleware
ros2 doctor -iw

# ros2 wtf: -r, -rf, -iw, hello
ros2 wtf
ros2 wtf -r
ros2 wtf -rf
ros2 wtf -r | grep middleware
ros2 wtf -iw

# ros2 interface: list, package, packages, proto, show
ros2 interface
ros2 interface list
for PACKAGE in $(ros2 interface packages)
do
    ros2 interface package $PACKAGE
done

PACKAGES=$(ros2 interface packages)
PROTOS=""
for PACKAGE in $PACKAGES
do
    PROTOS+=$(ros2 interface package $PACKAGE)
    PROTOS+=" "
done

echo $PROTOS

for PROTO in $PROTOS
do 
    echo $PROTO
    ros2 interface proto $PROTO
done

INTERFACES=$(ros2 interface list)
for INTERFACE in $INTERFACES
do
    echo $INTERFACE
    ros2 interface show $INTERFACE
done

# ros2 launch: <package, launchfile>, <full path to launch file>
#ros2 launch demo_nodes_cpp add_two_ints.launch.py
#ros2 launch demo_nodes_cpp add_two_ints_async.launch.py
#Issue: ros2 launch demo_nodes_cpp add_two_ints_async.launch.xml

# ros2 multicast: received, send
ros2 multicast receive &
ros2 multicast send

# ros2 node: info, list

# ros2 param: delete, describe, dump, get, list, set

# ros2 pkg: create, executables, list, prefix, xml
PACKAGES=$(ros2 pkg list)
for PACKAGE in $PACKAGES
do
    echo --$PACKAGE
    ros2 pkg prefix $PACKAGE
    ros2 pkg xml $PACKAGE
    ros2 pkg executables $PACKAGE
done

ros2 pkg create ros2-cli-testing.tmp
cat ros2-cli-testing.tmp/package.xml
cat ros2-cli-testing.tmp/CMakeLists.txt
rm -r ros2-cli-testing.tmp

# ros2 run: --prefix
ros2 run --prefix "timeout 10" demo_nodes_cpp talker

# ros2 security: linux_demo, macos_demo, windows_demo
# TODO

# ros2 service: call, find, list, type
ros2 run demo_nodes_cpp add_two_ints_server &
ros2 service list
ros2 service find add_two_ints
ros2 service type /add_two_ints
ros2 run demo_nodes_cpp add_two_ints_client
ros2 service call /add_two_ints example_interfaces/srv/AddTwoInts "{a: 1, b: 2}"
pkill -f add_two_ints
ros2 daemon stop

# ros2 test
ros2 test /opt/ros/$ROS_DISTRO/share/launch_testing_ros/examples/talker_listener_launch_test.py

# ros2 topic: bw, delay, echo, find, hz, info, list, pub, type

# ros2 trace
