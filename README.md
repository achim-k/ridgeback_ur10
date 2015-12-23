# ridgeback_ur10
Driver and config package for UR10 on the Ridgeback

To properly send and receive ROS messages for your computer, four things must be setup correctly:
1.	The /etc/hosts file on the Ridgeback must contain and entry with your computer’s hostname and IP address
2.	Similarly, the /etc/hosts file on your computer must contain an entry for the Ridgeback
3.	Your computer must have “export ROS_MASTER_URI=http://HOSTNAMEOFROBOT:11311” in every new terminal window.
4.	Your computer must have “export ROS_IP=[YOUR.IP.HERE]” in every new terminal window.

Once these settings are properly done, execute a rostopic echo on a topic to verify that data is correctly coming through.
Software Information 
•	All nonstandard ROS packages are located in ~/catkin_ws.
•	This system is pre-configured to start a joystick interface node for teleoperation. At any time, the wireless gamepad may be used to drive the Ridgeback.  Hold down the top left shoulder button, and use the left analog stick to control Ridgeback.
•	The hardware launch script will run on startup. It can be started in the background with sudo service ros start and stopped with sudo service ros stop. It may be launched in the foreground using sudo ros-start.  Your team should never need to start or stop the service—just use roslaunch to launch additional nodes which interface with the persistent ones.

Connection to UR10
The UR10 must be powered on, and enabled with the UR10 teach pendant. This can be verified by manually moving the arm with the “Run Program” -> “Move” menu.

If everything has come up correctly, you should be able to echo /joint_states to see the current real time position of all joints.
The user can also stow the arm by running on the Ridgeback “rosrun ur_modern_driver stow_ur10.py”. Not that this script is not stable in all positions, as it juts blindly executes joint angle commands.
Using Moveit
To use moveit, the user’s laptop must be connected to the Ridgeback and configured as above.

Clone the following git repository to the user’s computer https://github.com/ibaranov-cp/ridgeback_ur10.git and catkin_make and then source.

With the launch file, the user can call “roslaunch ridgeback_ur10_moveit ridgeback_ur10_planning_execution.launch”. If installation has been done correctly, no errors should appear, and the words “All is well! Everyone is happy! You can start planning now!” should be in green. The user can now start to plan using MoveIt!

To launch a nice user interface, open a new terminal window on the user computer, execute the steps in Network Information, and then execute “https://github.com/ibaranov-cp/ridgeback_ur10.git” The following window should appear (with a Ridgeback instead of a Husky). In the “Planning” tab, set the Start State to current, and the Goal state to random valid. The orange goal state should be solid orange, not red (try a few different ones). Once ready, click plan, and a preview of the arm motion will appear. When ready, and with a hand on the UR10 E-STOP, click Execute. The arm should move to the planned position.
