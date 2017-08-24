## Dragon DDK Description
This is a ROS package that includes the STL mesh and URDF for the Dragon Drone Development Kit available [here](https://worldsway.com/product/dragon-drone-development-kit/).  The URDF allows the robot_state_publisher ROS package to publish the useful coordinate frames for the target and tell other ROS packages where to find the 3d mesh file.

### Git Setup
To install, clone this repo to your workstation.  It is easiest to compile ros packages on target with a ROS envrionment set up.

After cloning, either copy this directory to your catkin workspace (probably /home/linaro/catkin_ws/src/) or use git!  This is my preferred method.
Although your target won't be able to access the gitlab, it should be able to access your workstation.  After cloning the git repo on your workstation, ssh into the target and run:
```bash
cd /home/linaro/catkin_ws/src/
git clone ssh://YOUR_USER_NAME@YOUR_IP_ADDRESS/PATH/TO/THE/GIT/REPO
```
for example, I run:
```bash
git clone ssh://mshomin@192.168.1.77/Users/mshomin/Desktop/gitstage/dragon_ddk_description
```
This allows you to make changes on your target and push them to your workstation, make change on your workstation and pull them from target, and still push back to the gitlab remote.
Note that if you make changes on target and push, you'll have to push again from your workstation to update them on gitlab.

### Dependencies
Now that you have the repo, we'll need some dependencies form aptitude.
On target, run:
```bash
rosdep install dragon_ddk_description
```

### Testing
Make sure your target has its ROS_IP environment variable set:
```bash
export ROS_IP=192.168.1.1
```
This IP assumes softap mode.  Now run the example file:
```bash
roslaunch dragon_ddk_description test_urdf.launch
```
On your workstation (with ROS installed) set you ROS env variables and run RVIZ
```bash
export ROS_MASTER_URI=http://192.168.1.1:11311
rosrun rviz rviz
```
Set your fixed frame to "/base_link" and add 2 display types: TF, and RobotModel.
You should see a mesh of the quadrotor and coordinate frames for its cameras and IMU.