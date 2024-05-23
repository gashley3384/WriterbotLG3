
# WriterbotLG3

### PROJECT DESCRIPTION
This project is a robot that writes out letters in a created language called Angarkase according to keyboard inputs put in by a person. You will be able to input a letter, and a small plate
with a piece of paper will move with a pen over it, which will be attached to a servo in order to lift and put down the pen. 

### ONSHAPE LINK

(https://cvilleschools.onshape.com/documents/d0332011792ff0881e4ecb2d/w/f60ced9a74de595b67e1cf04/e/22963176449209f64e9ac10e?renderMode=0&uiState=664fa3f58b969a737dabac27)

### 

### CODE COMPLEX
```python
import board
import time
import digitalio
from adafruit_motor import stepper 
from adafruit_motor import servo 
import pwmio 
#these are the necessary libraries

#Little explanation for corexy system for anyone who is unfamiliar
#2 motors, connected to a slider(x-direction) on top of another slider(y-direction)
#if 1 motor moves, the system should move the x slider diagonally 
#if both motors move and they are both traveling in the same direction, x slider moves left/right
#if both motors move in opposite directions x slider moves up/down
#with one speed, this allows for 8-directional motion


DELAY = 0.01
FULLTURN = 200 #Stepper has up to 200 steps, few variable
HALFTURN = 100
QTURN = 50 #quarter turn
ETURN = 25 #eighth turn
letnum = 0  #number of letter, allows for going to the next line + move down
linenum = 0 #number of line, allows count line

 
coils1 = (
    digitalio.DigitalInOut(board.D9),  # A1
    digitalio.DigitalInOut(board.D10), # A2
    digitalio.DigitalInOut(board.D11), # B1
    digitalio.DigitalInOut(board.D12), # B2
) # we gotta set up those coils

for coils in coils1:
    coils.direction = digitalio.Direction.OUTPUT #motor is the output


motor1 = stepper.StepperMotor(coils1[0], coils1[1], coils1[2], coils1[3], microsteps=None) #motor setup stuff

coils2 = (
    digitalio.DigitalInOut(board.D4),  # A1
    digitalio.DigitalInOut(board.D5), # A2
    digitalio.DigitalInOut(board.D6), # B1
    digitalio.DigitalInOut(board.D7), # B2
) # we gotta set up those coils for the second motor
#for the second motor instead of coils1 and motor1, use coils2 and motor2

for coils in coils2:
    coils.direction = digitalio.Direction.OUTPUT

motor2 = stepper.StepperMotor(coils2[0], coils2[1], coils2[2], coils2[3], microsteps=None)

pwm = pwmio.PWMOut(board.D2, duty_cycle=2 ** 15, frequency=50) #servo setup stuff

my_servo = servo.Servo(pwm) #naming the servo

#FUNCTION GUIDE:
#the ones that start with s are the servo ones
#the other ones are the motor ones\
#first word(s) is direction, the second bit is how much of a turn it is
#1 is full, 2 is half, etc.. 

def right1(): #defines the function name
    for step in range (FULLTURN):   #variable in parens is how far it goes
        motor2.onestep(style=stepper.DOUBLE) #motor 2 goes forwards
        motor1.onestep(style=stepper.DOUBLE) #motor 1 goes forwards
        time.sleep(DELAY)

def right2 ():
    for step in range (HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def right4 ():
    for step in range (QTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def left1 ():
    for step in range (FULLTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def left2 ():
    for step in range (FULLTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def left4 ():
    for step in range (QTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def up1 (): #up here is towards the motors
    for step in range (FULLTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def up2 ():
    for step in range (HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def up4 ():
    for step in range (QTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def down1 ():
    for step in range (FULLTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def down2 ():
    for step in range (HALFTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def down4 ():
    for step in range (QTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def upright1 ():
    for step in range(FULLTURN):
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def upright2 ():
    for step in range(HALFTURN):
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def upright4 ():
    for step in range(QTURN):
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def downleft1 ():
    for step in range(FULLTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def downleft2 ():
    for step in range(HALFTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def downleft4 ():
    for step in range(QTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def upleft1 ():
    for step in range(FULLTURN):
        motor2.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)
 
def upleft2 ():
    for step in range(HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def upleft4 ():
    for step in range(QTURN):
        motor2.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def downright1 ():
    for step in range(FULLTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def downright2 ():
    for step in range(HALFTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def downright4 ():
    for step in range(QTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def sup ():
    my_servo.angle = 50

def sdown ():
    my_servo.angle = 46


while True:
    x = input("Enter command: ") #keyboard setup stuff, x is the variable that holds letters
    print(letnum)
    if x is ("k"): #if you type in k when asked for a command, robot will move
        downright2() #down and to the right half turn(diagonal) 
        up4() #up quarter turn
        sup() #servo arm up
        letnum = letnum + 1
    if x is ("w"):
        up2()
    if x is ("a"):
        left2()
    if x is ("s"):
        down2()
    if x is ("d"):
        right2()
```

### CODE SIMPLE

```python
import board
import time
import digitalio
from adafruit_motor import stepper 
from adafruit_motor import servo 
import pwmio 
#these are the necessary libraries

DELAY = 0.01
FULLTURN = 200 #Stepper has up to 200 steps, few variable
HALFTURN = 100
QTURN = 50 #quarter turn
ETURN = 25 #eighth turn
letnum = 0  #number of letter, allows for going to the next line + move down
linenum = 0 #number of line, allows count line

 
coils1 = (
    digitalio.DigitalInOut(board.D9),  # A1
    digitalio.DigitalInOut(board.D10), # A2
    digitalio.DigitalInOut(board.D11), # B1
    digitalio.DigitalInOut(board.D12), # B2
) # we gotta set up those coils

for coils in coils1:
    coils.direction = digitalio.Direction.OUTPUT #motor is the output


motor1 = stepper.StepperMotor(coils1[0], coils1[1], coils1[2], coils1[3], microsteps=None) #motor setup stuff

coils2 = (
    digitalio.DigitalInOut(board.D4),  # A1
    digitalio.DigitalInOut(board.D5), # A2
    digitalio.DigitalInOut(board.D6), # B1
    digitalio.DigitalInOut(board.D7), # B2
) # we gotta set up those coils for the second motor
#for the second motor instead of coils1 and motor1, use coils2 and motor2

for coils in coils2:
    coils.direction = digitalio.Direction.OUTPUT

motor2 = stepper.StepperMotor(coils2[0], coils2[1], coils2[2], coils2[3], microsteps=None)

pwm = pwmio.PWMOut(board.D2, duty_cycle=2 ** 15, frequency=50) #servo setup stuff

my_servo = servo.Servo(pwm) #naming the servo

#FUNCTION GUIDE:
#first letter + number indicates type of motor and motor number
#s is servo, m1 is motor 1 and m2 is motor 2
#f or b defines forwards or backwards for motor
#up or down is for servo up or servo down

def m1f ():
    for step in range(HALFTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m1b ():
    for step in range(HALFTURN):
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def m2f ():
    for step in range (HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m2b ():
    for step in range(HALFTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def left():
    for step in range (HALFTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def right():
    for step in range (HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def mup():
    for step in range (HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def mdown():
    for step in range (HALFTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def sup ():
    my_servo.angle = 50

def sdown ():
    my_servo.angle = 45


while True:
    x = input("Enter command: ") #keyboard setup stuff, x is the variable that holds letters
    if x is ("q"):
        m1f()
    
    if x is ("w"):
        m1b()

    if x is ("e"):
        m2f()

    if x is ("r"):
        m2b()
    
    if x is ("c"):
        left()
    
    if x is ("z"):
        right()

    if x is ("s"):
        mup()

    if x is ("x"):
        mdown()

    if x is ("up"):
        sup()

    if x is ("down"):
        sdown()
    
    if x is ("test"):
        mup()
        time.sleep(DELAY)
        mdown()
        time.sleep(DELAY)
        left()
        time.sleep(DELAY)
        right()
        time.sleep(DELAY)
        m2b()
        time.sleep(DELAY)
        m2f()
```

### ONSHAPE LINK
(https://cvilleschools.onshape.com/documents/d0332011792ff0881e4ecb2d/w/f60ced9a74de595b67e1cf04/e/22963176449209f64e9ac10e?renderMode=0&uiState=66314a3d5f4708045409fd3d)
