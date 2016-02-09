# HCI Lab Notes

## My Keepon
 * [https://github.com/hariharsubramanyam/arduino_ros_led_keepon_control](https://github.com/hariharsubramanyam/arduino_ros_led_keepon_control)
 
## Kinova
* Supported on ROS
* Should work w/ Gazebo

## ROS - rviz issues
* [Blocked on install](http://answers.ros.org/question/202319/blocked-on-the-install-tutorial-naoqi_driver-not-found/)
* [Possible help](https://groups.google.com/forum/#!topic/ros-sig-aldebaran/9fRy1nPS0jA)
* Rviz test: `roslaunch nao_description display.launch`

## Perlin Noise
* Really good blog post explaination: [here](http://flafla2.github.io/2014/08/09/perlinnoise.html)

## MoveIt
* [explaination of current status of two repos/moveit-nao](https://groups.google.com/forum/#!topic/ros-sig-aldebaran/9fRy1nPS0jA)

## How-To
### Launch simulated Nao
* with moveit: change ip to 127.0.0.1 (localhost) in `nao_dcm_robot/nao_dcm_bringup/config/nao_dcm.yaml`, set envr var `NAO_IP` to `127.0.0.1` (localhost), run `roslaunch nao_gazebo_plugin nao_gazebo_plugin_H25.launch`

## Time/Findings/Misc
### 1/29/16 week
* Not much ROS support for Keepon, could look into that repo, though
* Went ahead and installed MoveIt, looks like it's used freq with Gazebo... and should help me get acclimated w/ actual Nao, simulation, etc
* Made post w/ local rviz simulation issues
* Installed Gazebo, can now plan motions with MoveIt!, next step on real Nao?
* Now looking how to go about integrating the perlin noise - ROS plugin/node? Modular?
    * Getting the previous Gaze Aversion code running would likely help in understanding how Perlin was implemented... so off to Windows.

### 2/1/16 week
* 2/2: Gaze aversion working - looked through the code for a while to see how the Perlin ties into everything... while I'm here I'm going to start attemping to get the NAO/ROS working
    * Note: ROS indigo works with NAOqi 2.1.1... 
    * nao_dcm_bringup introduces weird twitching
    * nao_bringup works as expected - can see physical nao in rviz... yay
    * to bring up nao and view in rviz : `roscore` `roslaunch nao_bringup nao_full.launch nao_ip:=192.168.1.201 roscore_ip:=10.211.55.3` and then `rosrun rviz rviz`
    * test walking: `rosrun teleop_twist_keyboard teleop_twist_keyboard.py`
    * this? [message_filters ROS plugin](http://wiki.ros.org/message_filters?distro=indigo)
    *

## Todo (1/29/16)
* [ x ] Gaze aversion
* [ x ] ROS with physical nao
* [ ] filtering messages... simulate nao and view messages... 
* attempt ROS topic transform
* creating idle motion, look at gaze aversion
* make sure head motion works
* doc out sending to topics, which topics, etc
* add new branch to gaze aversion
