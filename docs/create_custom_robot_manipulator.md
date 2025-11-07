# Creating Custom Robot in Fusion360

## Introduction

In robotics, we need a way to describe our robot (its shape, size, joints, and links) so that simulators and control software can use it.  
This description format is called **URDF** (Unified Robot Description Format).  



In this tutorial, you will:
<!-- TOC -->
* [Model a simple mobile robot manipulator in **Fusion360**](#model-a-simple-mobile-robot-manipulator-in-fusion360)

* [Convert the design into **URDF format**](#convert-the-design-into-urdf-format)

* [Prepare it for use in simulators such as **Isaac Sim** or **Gazebo**](#prepare-it-for-use-in-simulators-such-as-isaac-sim-or-gazebo)
 
<!-- TOC -->


By the end, you’ll have your own robot model ready for simulation 🚀  



## Before You Start

- Make sure you have **Autodesk Fusion360** installed.    
- Have a basic understanding of sketches in Fusion360.  

---

## Rules for Creating Robots in Fusion360

When modeling a robot in Fusion360, there are a few important rules to follow so that the robot can be successfully exported to URDF and work correctly in simulation:

1. **Separate each moving part into its own body**  
   - Example: The chassis, each body, and the lidar should all be **separate bodies**.  

2. **Rename bodies clearly**  
   - This makes it easier to manage later.  
   - Example: `base_link`, `link_1`, `link_2`, etc.  

3. **Convert bodies into components**  
   - URDF requires components (links) rather than raw bodies.  

4. **Add joints between moving parts**  
   - For link_1, we will add **revolute joints** so that they can rotate.  

5. **Define materials for each component**  
   - Materials provide physical properties (like mass and friction) used by the simulator.  





=============================

# Model a simple mobile robot manipulator in **Fusion360**

In Fusion360, create a new sketch, and in Fusion360,

1. ### Create the base_link of the robot:
    - Start by creating a new sketch on the XY plane.

    - Select a rectangle on a workspace.

    ![sketch](/png/png/1.png)

    - Draw a rectangle on a XY plane with dimension 300 x 300

    ![sketch plane](/png/png/2.png)

    - Finish this sketch and extrude it on 300mm

    ![sketch plane](/png/png/3.png)

    - Select this model and right click on it. Create the component from this body and name it base_link

    ![base_link](/png/png/4.png)

    - Select on the top of this rectangle and create a new sketch. On this new sketch create new rectangel with dimension 245 x 30 as shown in this picture.

    ![base_link](/png/png/5.png)

     - Make same way in the left side.

    ![base_link](/png/png/6.png)

     -Extrude it on 300 mm

    ![base_link](/png/png/7.png)

     -Create the sketch on a right side of this triangle

    ![base_link](/png/png/8.png)

    -Draw the circle with diameter 140 mm. 

    ![base_link](/png/png/9.png)

    -Extrude this circle till it reach to the next rectangle. 

    ![base_link](/png/png/10.png)

    Select this circle and choose the construct. In this construct select tangent plane

    ![base_link](/png/png/11.png)

    In this construct select tangent plane

    ![base_link](/png/png/12.png)

    When you selected this assembler. You can see a new plane which we gonna rotate to suitable degree. Rotate it to -45 degree

    ![base_link](/png/png/13.png)

    Select this plane and create a new sketch

    ![base_link](/png/png/14.png)

    Create the new rectangle 100x180

    ![base_link](/png/png/15.png)

    Extrude it on 600 mm
    ![base_link](/png/png/16.png)

    Select the top of this rectangle and create new sketch
    ![base_link](/png/png/17.png)

    Create on this sketch new rectangle 17x80 mm

    ![base_link](/png/png/18.png)

    Make a same way on left side of rectangle

    ![robot](/png/png/19.png)

    Extrude it on 100 mm

    ![extrusion](/png/png/20.png)

    Make sure that your rectangle combined with your cylinder to make dependencies.

    ![base_link](/png/png/21.png)

    Extrude to 20 mm
    ![base_link](/png/png/22.png)

    Let's create a new joint. Create a new sketch

    ![base_link](/png/png/23.png)

    Draw the circle with Diameter 50 mm

    ![base_link](/png/png/24.png)

    Extrude this circle on 150 mm

    ![base_link](/png/png/25.png)
    
    Click on COnstruct and tangent plane

    ![base_link](/png/png/26.png)
        
    Rotate this plane on -5 degree

    ![base_link](/png/png/27.png)
            
    Click on create the sketch and draw the rectangle 30x110 mm.

    ![base_link](/png/png/28.png)
                
    Extrude it to 400 mm

    ![base_link](/png/png/29.png)
                    
    Locate to your base_link and right click on it. Select ground from parent

    ![base_link](/png/png/30.png)
                        
6. ### Rename the Bodies
    - In the Browser panel (left-hand side of Fusion360), expand the Bodies folder.

    - Right-click on each body and create components from body
    - In my case:
        ```
        Body1 → base_link 

        Body2 → link_1

        Body3 → link_2
        ```
# Add revolute joints to robot

1. ### Let's add revolute joints to each wheel, so that it was able to rotate
    - Press J on your keyboard to open the Joint tool. (English Keyboard).   Alternatively, you can access it from the Assemble → Joint menu.

    - Define the Joint for a links
        ```
        Select links_1 → Click on the center of cylinder 

        Select base_link → Click on the origin of the corresponding axle.

    - ![base_link](/png/png/32.png)

    - ![base_link](/png/png/33.png)

    -  Repeat for All links


2. ### Assign Materials to the Robot
    - In the **Browser panel**, right-click on any component (e.g., `base_link`) and select **Physical Material**.  
    - In the **Physical Material window**, drag and drop materials from the library onto the robot’s parts:  
        - `base_link` → Metal (e.g., Aluminum or Steel)  
        - links → steel (or ABS Plastic for rims)  
    - Repeat the process for all components until each has a defined material.  
     - ![base_link](/png/png/45.png)

# Convert the design into **URDF format**

Now, As the robot is ready, let's install the fusion2urdf add-in:

## Install Fusion2URDF Add-In

1. Go to the fusion2urdf GitHub page: [https://github.com/syuntoku14/fusion2urdf](https://github.com/syuntoku14/fusion2urdf) 

2. Click the green **Code** button.  

3. In the dropdown, select **Download ZIP**

![download add-in ]- ![ready](/png/png/50.png)


### Install fusion2urdf Add-in
Unzip the downloaded package. Run the following commands in your shell, depending on your operating system:  

#### Windows (PowerShell)
```powershell
cd <path to fusion2urdf>

Copy-Item ".\URDF_Exporter\" -Destination "${env:APPDATA}\Autodesk\Autodesk Fusion 360\API\Scripts\" -Recurse
```

#### macOS (bash or zsh)
```powershell
cd <path to fusion2urdf>

cp -r ./URDF_Exporter "$HOME/Library/Application Support/Autodesk/Autodesk Fusion 360/API/Scripts/"
```

---
## Export Robot as URDF
As you have installed the Fusion2URDF add-in: 

1. In Fusion 360, go to **Utilities → Add-Ins → Scripts and Add-Ins**.  
2. From the list, select **URDF_Exporter**.  
3. Choose the export directory where you want to save your URDF files.  
4. Save the settings.  
5. You should see a confirmation message indicating that the URDF was installed successfully.  
![download add-in ](/png/png/52.png)

---
# Prepare it for use in simulators such as **Isaac Sim** or **Gazebo**

One Last Step left:

### Finalize the URDF

1. Navigate to the directory where you saved the robot description.  
2. Inside the **urdf/** folder, locate the exported file.  
3. Change the file extension from **.xacro** to **.urdf**.  

---

# ✅ Now your robot model is ready!


