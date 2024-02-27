## Scope
The goal of our project is to create a robot arm that lifts up and down while holding a writing implement so that it writes in Angerkase on a piece of paper held by the robot arm opposite of it.
Once we can control the writing utensil/paper and get the input separately, we will make it write in Angarkase.
The project is challenging.


## Schedule
Week 1: CAD Pen Mount and Paper mount plate
Week 2: CAD Baseplate and Begin CADing Mechanism
Week 3: Finish CADing mechanism prototype and print over weekend
Week 4: Assemble and test. If bad → fix and reprint; else → begin Code
Week 5: Continue code and CAD pen holder and print prototype
Week 6: Finish base functions (MoveX, MoveY) and if prototype works → MoveZ
Week 7: codeNewline function and begin writing translate function
Week 8: continue writing translate function
Week 9: finish writing translate function
Week 10: testing and editing
Week 11: documenting
Week 12 (week after APs): documenting

##Sketch
CoreXY on Prusa printables is inspiration



## BOM
Stepper motors
Servo motor
Baseplate
Gears
Paper mount plate (it moves)
Connector strip
Pen mount
Pen
Screws
Paper
Axles



## Pseudocode
### Function moveX:
	Moves the paper east/west depending on func input

### Function moveY:
	Moves the paper north/south depending on func input

### Function moveZ:
	Moves the writing utensil up/down depending on func input

### Function translate:
	Writes out an individual Angarkase letter depending on func input
	Using moveX, moveY, and moveZ

### Function newLine:
	Moves paper to the right and draws a vertical line, ending at the top
	Using moveX, moveY, and moveZ
	

Ask about what needs to be written
Get input
For each letter in input
	if there is no space on the paper (we know the size), go to a new line
	translate(letter)

### Problem
There is no standardized way to write Angarkase. This robot would make it so that we could replicate each symbol in exactly the same way consistently. 

### Other Designs
- Physics Robot Launcher
- Instrument playing robot
- Typing Robot
- Paper Airplane Robot
- Math Solving Robot

