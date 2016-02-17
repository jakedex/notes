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

## Robotics, misc, new terms/concepts
* urdf: Unified Robot Description Format- an XML format for representing a robot model
* teleoperation, teleops: 'remote control'
* odometry: use of motion data to estimate change in position over time
* tf: keeps track of coordinate frames, allows user to simply transform points, vectors, etc between any two coordinate frames 
* localization: 'where in environment is the robot and what is the robot's orientation in that environment?'

## MoveIt
* [explaination of current status of two repos/moveit-nao](https://groups.google.com/forum/#!topic/ros-sig-aldebaran/9fRy1nPS0jA)

## How-To
### Launch simulated Nao
* in gazebo: change ip to 127.0.0.1 (localhost) in `nao_dcm_robot/nao_dcm_bringup/config/nao_dcm.yaml`, set envr var `NAO_IP` to `127.0.0.1` (localhost), run `roslaunch nao_gazebo_plugin nao_gazebo_plugin_H25.launch` then `rosrun rviz rviz`
* with naoqi and nao\_bringup: first start naoqi with `naoqi/naoqi-sdk-2.1.2.17-linux64/naoqi --verbose --broker-ip 127.0.0.1` and then the driver pointing to the simulated robot with `NAO\_IP=127.0.0.1 roslaunch nao_bringup nao_full_py.launch` or `roslaunch naoqi_driver_py naoqi_driver.launch` (I was having issues with the cpp driver...)
    * load model in rviz: `roslaunch nao_description robot_state_publisher.launch` and finally, `roslaunch rviz rviz`. then once in rviz, you'll need to follow the steps described under "Viewing the simulated Nao robot in rviz" [here](http://wiki.ros.org/nao/Tutorials/Getting-Started)

### Launch Physical Nao in rviz
* to bring up nao and view in rviz : `roscore` `roslaunch nao_bringup nao_full.launch nao_ip:=192.168.1.201 roscore_ip:=10.211.55.3` and then `rosrun rviz rviz`

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
    

### 2/8/16 week
* nao\_bringup and nao\_dcm\_bringup use different controller/publishing methods.. could result in issues as I'm only able to simulate with dcm
* gazebo simulates all the Nao sensors with plugins
* nao\_bringup uses naoqi\_bridge's naoqi\_driver, this node publishes all sensor/actuator/battery/temp data to their corresponding topics, and subscribes to RVIZ simple\_goal and cmd\_vel for teleop
* nao\_dcm stack doesn't use such driver, it 'connects' directly to the robot, not through the API that Aldebaran implemented with their driver
* looked into using [tf](http://wiki.ros.org/tf) and throwing transform data through perlin - but that limits the support to mostly distributed systems
* whew, in the process, managed the get nao\_bringup to work by using the python SDK. Which is big as this *hopefully* resolves any issues I would have had with the nao\_dcm stack vs naoqi.
* the /naoqi\_joint\_states node is publishing on the /joint\_states topic to the /naoqi\_moveTo node. the /naoqi\_joint\_states node simply reads in joint data from the Aldebaran API
* interesting... [http://www.sc.ehu.es/ccwrobot/papers/rodriguez14humanizing.pdf](http://www.sc.ehu.es/ccwrobot/papers/rodriguez14humanizing.pdf)
* /naoqi\_moveto node subscribed to topic /move\_base\_simple/goal, sending geometry_msgs/PoseStamped (basically raw positon/orientation) which is what we (likely) want to publish to
* So, as of now, I'm positive it'll be possible to filter all/most data being sent to the robot, but what I question is how much it actually sent vs interpretted locally, that's where we could have issues. The Gaze aversion project is obviously different as it runs locally. I suppose I need to investigate the api communication, specifically the following model: pub\_node->message/topic->sub\_node to determine what the sub\_node is saying to the API.
    * Also, the above brings up questions about the ROS package's generality - if simple, higher level, message/node/topic implementation isn't really viable, that means specialized config for each machine... 
    * update: cmd_vel/teleop filtering is out of the question, the messages are only send once/vel change (makes sense)
* Maybe tf/robot\_states deserve another look, what if we just 'perlinize' incoming state/odometry data so that tf bases future states on this already filtered state? is that even possible? pose to pose basis, just transform poses?
* Currently: looking at the /move\_base\_simple/goal
    * where are my controllers? is that only dcm? or only physical? am i missing a package?

### 2/15/16 week
* the nao\_driver package has been replaced with nao\_bringup and nao\_robot. the nao\_controller, aka node i was looking for last week, was deprecated with the switch to bringup and robot. to my understanding, all of the controller's functionality now lies in naoqi\_pose, which listens for joint states along with actionlib goals (tbd). 
* to move individual joints, can either send goals (geometry\_msgs with actionlib) on topic move\_base\_simple/goal to naoqi\_posecontroller node. Or, send sending joint angle with speed messages on the /joint\_angles topic to the pose\_controller node
    * `rostopic pub /joint_angles naoqi_bridge_msgs/JointAnglesWithSpeed -- '[ 1, now, Head]' '[HeadYaw,HeadPitch]' '[1,-1]'  1.0  0`
* ![ROS Control map](http://wiki.ros.org/ros_control?action=AttachFile&do=get&target=gazebo_ros_control.png)
* All (most? aside from moveit/gazebo?) ROS navigation commands are sent either in the form of individual messages of type joint\_trajectory (joint name, coordinates), or actionlib through geometry\_msg types (need to read up on actionlib)
* Currently looking into actionlib, joint\_trajectory, and trajectory filters

### Misc
* figure out how to implement
   * add on filter to pose\_controller? - not general
   * actionlib - not sure if I have as precise of control, but this is definitely more general 
   * [https://github.com/ros-naoqi/naoqi_bridge/blob/master/naoqi_pose/nodes/pose_controller.py](https://github.com/ros-naoqi/naoqi_bridge/blob/master/naoqi_pose/nodes/pose_controller.py)
   * 

### Discuss w/ Sean
* No apparent damages other than what you had already noted, though I still need to test walking etc. 
* Implementation talk - features, etc. So we want to provide an idle motion, along with filtering all user invoked motion?

## Todo
* [x] Gaze aversion
* [x] ROS with physical nao
* [ ] filtering messages... simulate nao and view messages... 
* [x] attempt ROS topic transform
* [ ] creating idle motion, look at gaze aversion
* [x] make sure head motion works
* [ ] doc out sending to topics, which topics, etc
* [x] add new branch to gaze aversion
