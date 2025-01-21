# VirtualFixture

## Dependencies:
This module relies on the BreachWarning module, which is a part of SlicerIGT. For more details on compiling this 
module from source, please see the instructions on this page: https://slicer-ros2.readthedocs.io/en/latest/pages/limitations.html

## Instructions:

In a terminal launch the sawSensablePhantom program:
Note: replace _distribution with the version of ROS 2 that is in use (galactic, humble, ...), ros2_ws 
should be the workspace where sawSensablePhantom is compiled

```bash
source /opt/ros/_distrubution_/setup.bash
source ~/ros2_ws/install/setup.bash
cd ~/ros2_ws/src/cisst-saw/sawSensablePhantom/share
ros2 run sensable_phantom sensable_phantom -D -j sawSensablePhantomDefaultDevice.json 
```

In another terminal launch the robot state publisher:
```bash
source /opt/ros/_distrubution_/setup.bash
source ~/ros2_ws/install/setup.
ros2 launch sensable_omni_model omni.launch.py 
```

In order to use the BreachWarning module, edit the .ui file in the BreachWarning source code. In the "Tool tip (to RAS) transform" selector node, add
'vtkMRMLROS2Tf2LookupNode' to the string list of node types in the selector node.

Finally, launch Slicer with the sourced files to show the robot
```bash
source /opt/ros/galactic/setup.bash
source ~/ros2_ws/install/setup.bash
cd ~/dev/Slicer-SuperBuild-Release/Slicer-build/
```

Now, in Slicer navigate to the ROS2 module. Select "Add new robot", no need to change the pre-filled line entries, press "Load robot".

Drag and drop the scene in the module "Resources" file called "SphereConstraint.mrb".

Navigate to the BreachWarning module. Within this module:

1. Set the "TumorModel" as model to watch
2. Set the transform "ros2:tf2lookup:tipToStylus" as the Tool tip transform
3. Check the "Display line to closet point" box (IMPORTANT - the VF won't work if this isn't visible)


Now, switch to the "Virtual Fixture" module and select activate fixture. When the Tip of the Omni model intersects the sphere
you will feel resistance. To Release the arm if there is any weird behaviour, select "Release".

Email: laura.connolly@queensu.ca if you have any questions!
