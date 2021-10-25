# Research Track Assignment 2
# Done by Jerin Joy (Matricola: 5061530)

# Description of the Assignment:
The assignment is the development of a software architecture for the control of a mobile robot. The software uses the move_base and gmapping packages for localizing the robot and plan the motion.The program uses Gazebo and RViz which allows the user to view the robot simulation and to log and replay the logged sensor information; also uses SLAM, path planning and collision avoidance to acquire the user's request and makes the robot to execute one of the pre-defined behaviours. 

The program should be able to do the following things:

1. The robot moves randomly in the environment, by choosing 1 out of 6 possible target positions: [(-4,-3);(-4,2);(-4,7);(5,-7);(5,-3);(5,1)].

2. Asks the user for the next target position, checking that the position is on eof the possible six target positions, and the robot reaches it.

3. The robot starts following the external walls. 

4. The robot stops in the last position. 

# How the Mobile Robot is controlled:

The final_assignment package contains the scripts,launch files and other dependencies used to simulate the 3D environment and move the robot in it.The simulation_gmapping.launch file launches the house.world file environment. The important node main_code.py contains the python code which is responsible for the mobile robot simulation.

The simulation is done in the following steps:

1. For the first step, main_code.py node requests my_srv for a random target position between the range of 1 to 6. Then,the main node publishes the target positions to */move_base/goal* and check the the status of goal by subscribing to the topic */move_base/status*. When the robot reaches the target and the status of robot is displayed, the main node requests the user to input again.

2. For the second step, the user chooses one out of six possible target positions and publishes it to */move_base/goal*.

3. For the third step, the wall_follower service is generated through initialization of a service client to allow the robot to follow the external walls.

4. For the fourth step, the node stops all actions and stops the robot by publishing commands of zero velocity in topic */cmd_vel*.

In steps 3 and 4, the interface also allows the user to enter the same or different request at any point in this state.


# my_srv(server):

The server package my_srv contains the Cpp file finalassignment_server.cpp which contains the source code for generating random integer within a specified range and advertising it over the node /finalassignment. It uprovides a requests with two integers namely min and max, and returns one random integer target_index within this range in response.

# Simulation of the assignment is done by follwing commands:


1. In the command terminal, launch Gazebo and rviz by executing the following command:
```bash
roslaunch final_assignment simulation_gmapping.launch
```
2. In a new command line terminal, run the following command:
```bash
roslaunch final_assignment move_base.launch
```
3. In a new command line terminal, run the following command:
```bash
rosrun final_assignment wall_follow_service_m.py
```
4. In a new command line terminal, run the following command:
```bash
rosrun my_srv finalassignment_server
```
5. In a new command line terminal, run the following command:
```bash
rosrun final_assignment main_code.py
```
6. To display the computational graph of the system,run the following command:
```bash
rosrun rqt_graph rqt_graph
```

