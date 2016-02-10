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
* topic /joint\_angles is what nao\_controller node is subscribed to, likely what we'd want to filter/transform
* looked into using [tf](http://wiki.ros.org/tf) and throwing transform data through perlin - but that limits the support to mostly distributed systems
* whew, in the process, managed the get nao\_bringup to work by using the python SDK. Which is big as this *hopefully* resolves any issues I would have had with the nao\_dcm stack vs naoqi.
* the /naoqi\_joint\_states node is publishing on the /joint\_states topic to the /naoqi\_moveTo node (is this the controller that interfaces with the naoqi_driver?)
* Currently: figuring out what the /base\_footprint node is... looking for nodes/topics that could be generalized to other robots.

## Todo
* [x] Gaze aversion
* [x] ROS with physical nao
* [ ] filtering messages... simulate nao and view messages... 
* [ ] attempt ROS topic transform
* [ ] creating idle motion, look at gaze aversion
* [ ] make sure head motion works
* [ ] doc out sending to topics, which topics, etc
* [ ] add new branch to gaze aversion
