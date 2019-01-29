========================================================
                  BUBBLE SORT README
========================================================
	Author: Jacob Massaro

========================================================
                     What it Does
========================================================
	This code allows a user to enter up to 8 numbers,
effecting the height or 8 cubes. The user can then add the
cubes into the scene and sort them. There are two sorting
methods. The first sorts everything at once, the second sorts
the cubes one at a time.



========================================================
                   Scales Folder
========================================================

1. Cubes
	- This folder has 8 values you can scale between 0 and 15
	- If you do not put any value (0), no cube will appear
	- You can add up to 8 cubes, but they do not have to be in order
	- The cubes will be evenly spaced no matter what order you put them in


========================================================
                   Functions Folder
========================================================
1. Add Cubes
	- You can press this button after you have added the cubes you want
	- If there are already cubes on the screen, it will print to the console that you have to reset the cubes first

2. All at Once
	- Press this button after you have already added cubes to the screen, it won't allow you otherwise
	- This button sorts all of the cubes at once
	- It prints the to console the origianl and sorted heights

3. One at a Time
	- Press this button after you have already added cubes to the screen, it won't allow you otherwise
	- With every click, this button makes one movement in the sort
	- The green cube is the cube we are currently on until we reach the end of one pass
	- The cube at the end will stay green as it is sorted
	- Each time you press the button, it prints the new sorted order of the cubes

4. Reset
	- This button will get rid of all the cubes on screen
	- It will not work unless you have already added cubes to the screen