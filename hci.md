# HCI Lab Notes

## Useful Links
#### My Keepon
 * [https://github.com/hariharsubramanyam/arduino_ros_led_keepon_control](https://github.com/hariharsubramanyam/arduino_ros_led_keepon_control)

#### Kinova
* [ROS page](http://wiki.ros.org/jaco)
* Check out [actionlib](http://wiki.ros.org/actionlib) for potential queuing of commands/goals

#### [perlin_noise_filter](https://github.com/jakedex/perlin_noise_node) / [perlin_noise_node](https://github.com/jakedex/perlin_noise_filter)
* [ROS filters](http://wiki.ros.org/filters)
* [rosparam](http://wiki.ros.org/rosparam)
* [pluginlib](http://wiki.ros.org/pluginlib)
* [roslaunch](http://wiki.ros.org/roslaunch)
* [cpp parameter server](http://wiki.ros.org/roscpp/Overview/Parameter%20Server#Getting_Parameters)
* Potential node code structuring: [Sending joint commands with ROS](http://gazebosim.org/tutorials?tut=drcsim_ros_cmds&cat=drcsim)
* What I used as a template: [node_example](https://github.com/tdenewiler/node_example)
* Filter inspiration: [laser_filters](https://github.com/ros-perception/laser_filters)

#### ROS with NaoQi troubleshooting
* [Blocked on install](http://answers.ros.org/question/202319/blocked-on-the-install-tutorial-naoqi_driver-not-found/)
* [Possible help](https://groups.google.com/forum/#!topic/ros-sig-aldebaran/9fRy1nPS0jA)

#### Perlin Noise
* Really good blog post explaination: [here](http://flafla2.github.io/2014/08/09/perlinnoise.html)

#### MoveIt
* [explaination of current status of two repos/moveit-nao](https://groups.google.com/forum/#!topic/ros-sig-aldebaran/9fRy1nPS0jA)

#### TF
* a frame is simply a way to think about coordinates and data locally
* transform is basically the offset between two frames
* [move\_to.py](http://docs.ros.org/jade/api/naoqi_driver_py/html/src_2naoqi__driver_2naoqi__moveto_8py_source.html)
* use `rosrun tf view_frames` to create a diagram of the frames being broadcast by tf over ROS

## Robotics, misc, new terms/concepts
* _urdf_: Unified Robot Description Format- an XML format for representing a robot model
* _teleoperation, teleops_: 'remote control'
* _odometry_: use of motion data to estimate change in position over time
* _tf_: keeps track of coordinate frames (e.g. head frame and chest frame), allows user to simply transform points, vectors, etc between any two coordinate frames.
* _localization_: 'Where in environment is the robot and what is the robot's orientation in that environment?'

## How-To
### Launch simulated Nao
* in gazebo: change ip to 127.0.0.1 (localhost) in `nao_dcm_robot/nao_dcm_bringup/config/nao_dcm.yaml`, set envr var `NAO_IP` to `127.0.0.1` (localhost), run `roslaunch nao_gazebo_plugin nao_gazebo_plugin_H25.launch` then `rosrun rviz rviz`
* with naoqi and nao\_bringup: first start naoqi with `naoqi/naoqi-sdk-2.1.2.17-linux64/naoqi --verbose --broker-ip 127.0.0.1` and then the driver pointing to the simulated robot with `NAO\_IP=127.0.0.1 roslaunch nao_bringup nao_full_py.launch` or `roslaunch naoqi_driver_py naoqi_driver.launch` (I was having issues with the cpp driver...)
    * load model in rviz: `roslaunch nao_description robot_state_publisher.launch` and finally, `rosrun rviz rviz`. then once in rviz, you'll need to follow the steps described under "Viewing the simulated Nao robot in rviz" [here](http://wiki.ros.org/nao/Tutorials/Getting-Started)

### Launch Physical Nao in rviz
* to bring up nao and view in rviz : `roscore` `roslaunch nao_bringup nao_full.launch nao_ip:=192.168.1.201 roscore_ip:=10.211.55.3` and then `rosrun rviz rviz`

### Run perlin_noise_node/filter
* `roscore`
* `roslaunch perlin_noise_node default.launch`
* `rosservice call /nao_robot/pose/body_stiffness/enable "{}"`

### Useful Commands
* Graph current ROS nodes, their corresponding messages, and the connections between them: `rosrun rqt_graph rqt_graph`
* Test walking/movement with any robot that accepts Twist messages:  `rosrun teleop_twist_keyboard teleop_twist_keyboard.py`
* Publish simple motion command to selected Nao joints: `rostopic pub -1 /joint_angles naoqi_bridge_msgs/JointAnglesWithSpeed '{header: auto, joint_names: ["LAnklePitch", "RAnklePitch"], joint_angles: [0, 0], speed: 1}'`

## Todo
* publishing/packaging
  * [ROS cpp style guide](http://wiki.ros.org/CppStyleGuide)
  * dynamic reconfigure?
  * tests?
* code
  * .launch for various robots
  * programatically enable stiffness
  * scaling var
* Kinova
* ROS release?
  * Requires [documentation](http://wiki.ros.org/rosdoc_lite)
  * [Releasing a Package for the First Time](http://wiki.ros.org/bloom/Tutorials/FirstTimeRelease)
  * [A Full Guide To Releasing With Catkin](http://wiki.ros.org/bloom/Tutorials/FullGuideToFirstTimeRelease)
  * Double check dependencies [catkin/CMake Guide](http://docs.ros.org/api/catkin/html/howto/format2/building_libraries.html)



## Time/Findings/Misc
#### 1/29/16 week
* Not much ROS support for Keepon, could look into that repo, though
* Went ahead and installed MoveIt, looks like it's used freq with Gazebo... and should help me get acclimated w/ actual Nao, simulation, etc
* Made post w/ local rviz simulation issues
* Installed Gazebo, can now plan motions with MoveIt!, next step on real Nao?
* Now looking how to go about integrating the perlin noise - ROS plugin/node? Modular?
    * Getting the previous Gaze Aversion code running would likely help in understanding how Perlin was implemented... so off to Windows.

#### 2/1/16 week
* 2/2: Gaze aversion working - looked through the code for a while to see how the Perlin ties into everything... while I'm here I'm going to start attemping to get the NAO/ROS working
    * Note: ROS indigo _only works_ with NAOqi 2.1.1 (only one of the robots is running this - other two on NAOqi 1.0 or something)
    * nao_dcm_bringup introduces weird twitching
    * nao_bringup works as expected - can see physical nao in rviz... yay
    * to bring up nao and view in rviz : `roscore` `roslaunch nao_bringup nao_full.launch nao_ip:=192.168.1.201 roscore_ip:=10.211.55.3` and then `rosrun rviz rviz`
    * test walking: `rosrun teleop_twist_keyboard teleop_twist_keyboard.py`
    * this? [message_filters ROS plugin](http://wiki.ros.org/message_filters?distro=indigo)

#### 2/8/16 week
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

#### 2/15/16 week
* the nao\_driver package has been replaced with nao\_bringup and nao\_robot. the nao\_controller, aka node I was looking for last week, was deprecated with the switch to bringup and robot. to my understanding, all of the controller's functionality now lies in naoqi\_pose, which listens for joint states along with actionlib goals (tbd).
* to move individual joints, can either send goals (geometry\_msgs with actionlib) on topic move\_base\_simple/goal to naoqi\_posecontroller node. Or, send sending joint angle with speed messages on the /joint\_angles topic to the pose\_controller node
    * `rostopic pub /joint_angles naoqi_bridge_msgs/JointAnglesWithSpeed -- '[ 1, now, Head]' '[HeadYaw,HeadPitch]' '[1,-1]'  1.0  0`
* ![ROS Control map](http://wiki.ros.org/ros_control?action=AttachFile&do=get&target=gazebo_ros_control.png)
* All (most? aside from moveit/gazebo?) ROS navigation commands are sent either in the form of individual messages of type joint\_trajectory (joint name, coordinates), or actionlib through geometry\_msg types (need to read up on actionlib)
* Currently looking into actionlib, joint\_trajectory, and trajectory filters

#### 2/22/16 week
* Can send basic Twist messages but they're all relative to the current position

#### 2/28/16 week
* sidenote: So, went off on a tangent after learning more about tf and things are finally coming together. The joint states array of vel/pos/effort is translated into TF by robot\_state\_publisher. naoqi\_moveto listens for PoseStamped msgs on the //move_base_simple/goal. (in other words, listening for actionlib goals)
* That being said, pose\_controller is sub'd to /joint\_angles, would publishing to this work? (It's my understanding that most robots emphasis on robots do have some variant of /joint\_angles)
* We just want an idle guy to be moving around slowly w noise, specifically on a specified joint.
    * so we want to apply noise to any 'frame', joint etc, regardless of input
    * could be done with tf? yeah, and couldn't we just filter each? yeah. but we need to make sure we're receiving all of them constantly. honestly something like a filter between robot state publisher would be optimal, afaik.
    * or, joint\_states -> joint\_angles with gazebo guide below? (promising...)
        * [gazebo guide](http://gazebosim.org/tutorials?tut=drcsim_ros_cmds&cat=drcsim)
* for turtle\_bot sim, we just want tf pub to turtles's position plus perlin

#### 3/6/16 week
* base\_footprint is literally calculating and publishing the 'ground' frame
* [Implementing Perlin Noise in ROS](https://docs.google.com/document/d/1KJ_mjMWaNjuOcGqn9yt_yRn_FuvPcu4qsKEV4n8r59U/edit?usp=sharing)
* [pose\_controller](https://github.com/ros-naoqi/naoqi_bridge/blob/master/naoqi_pose/nodes/pose_controller.py)

#### 3/20/16 week
* `rostopic pub -1 /joint_angles naoqi_bridge_msgs/JointAnglesWithSpeed '{header: auto, joint_names: ["LAnklePitch", "RAnklePitch"], joint_angles: [0, 0], speed: 1}'`

#### 3/27/16 week
* Important distinction between Generator and NaoGaze Perlin implementations - Generator is calling the Noise function with a single, increasing, value. While the NaoGaze is passing the previous X,Y,Z positions to generate noise values.

#### 4/24/16 week
* Well, it's not smooth smooth on physical... needs work
    * will have to disable ALautonomousLife - Simply double tap chest btn
    * rate at which messages come in varies.. need some way to stablize this... a timer really would help. (or just use a different callback - timer..)

#### 5/1/16 week
* Action lib queuing
    * actionlib supports it, and even buffers, but it's up to the implementation of the server
    * nao's [pose controller](https://github.com/ros-naoqi/naoqi_bridge/blob/master/naoqi_pose/nodes/pose_controller.py) uses `SimpleActionServer`s, which are limited to only one goal - whenever there's an incoming goal, the current is canceled... [source](http://answers.ros.org/question/9776/action-server-with-more-than-one-action/)
