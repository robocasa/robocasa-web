## Quick start
**(Mac users: for these scripts, prepend the "python" command with "mj": `mjpython ...`)**

### Explore kitchen layouts and styles
Explore kitchen layouts (G-shaped, U-shaped, etc) and kitchen styles (mediterranean, industrial, etc):
```
python -m robocasa.demos.demo_kitchen_scenes
```

### Play back sample demonstrations of tasks
Select a task and play back a sample demonstration for the selected task:
```
python -m robocasa.demos.demo_tasks
```

### Explore library of 2500+ objects
View and interact with both human-designed and AI-generated objects:
```
python -m robocasa.demos.demo_objects
```
Note: by default this demo shows objaverse objects. To view AI-generated objects, add the flag `--obj_types aigen`.

### Teleoperate the robot
Control the robot directly, either through a keyboard controller or spacemouse. This script renders the robot semi-translucent in order to minimize occlusions and enable better visibility.
```
python -m robocasa.demos.demo_teleop
```
Note: If using spacemouse: you may need to modify the product ID to your appropriate model, setting `SPACEMOUSE_PRODUCT_ID` in `robocasa/macros_private.py`.