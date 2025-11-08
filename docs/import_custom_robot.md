Open and Start the Isaac Sim. 

```
cd ~/isaacsim
./isaac-sim.selector.sh
```

## Prepare for simulation
Open
File -> Import -> (Robot URDF File) -> click the robot

Before importing the model, modify the following parameters:
- Links: Movable Base (Mobile Robot), Static Base (Manipulator)
- Joint Configuration: Stiffness
- In the Table:
 - Target: Velocity (Mobile Robot), Position (Manipulator)

![Isaac_sim](/png/png/Isaac_1.png)

As you have modified the settings based on the type of your robot,
Import the Model


Let's add some environment as reference:

Click on Create workspace -> physics-> ground_plane

![Isaac_sim](/png/png/Isaac_2.png)

Load as reference

Let's rotate the robot, to the ground. Select your stage viewport


![Isaac_sim](/png/png/Isaac_3.png)

Rotate the object around the X-axis by 90° to align its orientation correctly.

![Isaac_sim](/png/png/Isaac_4.png)

## Simulation process

let's start our simulation

Open
Tools -> Robotics -> OmniGraph Controllers -> Joint Position

In Appeared menu click Add and select your robot

![Isaac_sim](/png/png/Isaac_5.png)

Make sure you selected your robot model. 

![Isaac_sim](/png/png/Isaac_6.png)



The Graphs section contains OmniGraph nodes used for defining logic and data flow in Isaac Sim, such as controllers and command interfaces for the robot.
Here, the JointCommandArray node is selected — it is responsible for sending position, velocity, or effort commands to the robot’s joints, allowing direct control of the manipulator’s movement.

![Isaac_sim](/png/png/Isaac_7.png)

To simulate your manipulator click on a Run button then give any value to your joints 

![Isaac_sim](/png/png/Isaac_9.png)