# ROS-Nodelet-Tutorial
A step by step tutorial of nodelets based on the ROS example and done with containers

There seems to be very few information on ROS nodelets. The one tutorial that you can find is in the ROS official page.
However to be frank, I find it complicated and hard to understand.

I have also build my own docker containers for ROS (and ROS2 too ;) ) so in this tutorial I will use all of those to build
a simple tutorial of how to do a ROS nodelet.

# Tutorial

1. First download the project **"ROS_files"** soon to be in this account. You will use this to generate your ROS containers (so you don't need to install ROS whatsoever). These set of files are to build your container so don't add anymore files to this folder

2. Here we start. Build a folder where your workspace will be. Something like **Plugin_ws** and build a folder inside of it called **src**.

3. Take the path of this folder (like *"/home/pi/Plugin_ws"*) and edit the file *load_env_var.sh* (see step 1) with that string as your MYCOMPLETEDIR

4. Open a terminal in the folder containing the script load_env_var.sh and run *build_run_kinetic.sh*.

5. Once finished, you are inside the docker container and ROS is operational for you. Without installing it, how about that?! And note that eventhough your terminal was in the one containing the ROS_files, now you are automatically in the one you built in step 2! Magic!

6. run *catkin_make*. You have created a workspace

7. Source your workspace by typing *source devel/setup.bash*

8. make sure by typing *echo $ROS_PACKAGE_PATH*. You have to see your workspace along with the original ROS

Take a break... Now we are going to build a package

9. Create a Package (in our case for the nodelet) by going to src (*cd src*) and typing *catkin_create_pkg nodelet_tutorial_math roscpp pluginlib std_msgs* 

10. cd to the previous directory (*cd ..*) and run *catkin_make* again

You have your package created. For some reason (TO INVESTIGATE) when you do all of this the folders created are locked. You will need to edit add or delete
these files so you should change permisions to chmod 777 to the folders or files you require

One thing to notice. **You need to run these commands from inside the container**. However notice that the container is synchronized with the contents of the folder created in step 2 *from outside the container*. So you could use your editor of choice to write your code inside those folders and it will be reflected inside the container as well. 

11. Go to the src folder *inside* the package (not only the one in the workspace but the one inside the package *nodelet_tutorial_math*) and write your nodelet 
    This nodelet is a class derived from *nodelet::Nodelet* and it has to have a public constructor withouth parameters and private methods: One virtual called *onInit* and if the nodelet has a subscriber another called *callback* (which is going to be the nodelet subscriber callback).
    It also could have all things a node can have, such as a Publisher or a Subscriber

  The *onInit* method has to have a *ros::NodeHandle* and it can get parameters,initialize publishers, subscribers, etc.
  
  One important thing. The nodelet has to have outside of the class the following declaration
  ```
  PLUGINLIB_EXPORT_CLASS(<namespace::Classname>, nodelet::Nodelet)
  ```
12. 



