
# Engr3robotarmLG

### PROJECT DESCRIPTION
This project is a robot that writes out letters in a created language called Angarkase according to keyboard inputs put in by a person. You will be able to input a letter, and a small plate
with a piece of paper will move with a pen over it, which will be attached to a servo in order to lift and put down the pen. 

### CODE COMPLEX
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

def m1f1 ():
    for step in range(FULLTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m1f2 ():
    for step in range(HALFTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m1f4 ():
    for step in range (QTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m1f8 ():
    for step in range(ETURN):
        motor1.onestep(direction=stepper.DOUBLE)
        time.sleep(DELAY)

def m1b1 ():
    for step in range (FULLTURN):
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def m2f1 ():
    for step in range(FULLTURN):
        motor2.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m2f2 ():
    for step in range(HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m2f4 ():
    for step in range (QTURN):
        motor2.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m2f8 ():
    for step in range(ETURN):
        motor2.onestep(direction=stepper.DOUBLE)
        time.sleep(DELAY)

def m2b1 ():
    for step in range (FULLTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def m2b2 ():
    for step in range (HALFTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)
def right():
    for step in range (HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)
def left():
    for step in range (HALFTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)


def sup ():
    my_servo.angle = 50

def sdown ():
    my_servo.angle = 46


while True:
    x = input("Enter command: ") #keyboard setup stuff, x is the variable that holds letters
    print(letnum)
    print(linenum)
    if x is ("k"): #if you input the letter in the "", the stepper will do these function
        sup()
        m1f1()
        time.sleep(.2)
        sdown()
        m1f2()
        letnum = letnum + 1 #uptick variable by 1
    if x is ("g"):
        sup()
        m1f4()
        letnum = letnum + 1
    if x is ("t"):
        m1b1()
        time.sleep(.5)
        sdown()
        m1f4()
        letnum = letnum + 1
    if x is ("d"):
        m1f8()
        time.sleep(.5)
        sdown()
        m1b1()
        letnum = letnum + 1
    if x is ("1"):
        m1f1()
    if x is ("2"):
        m2f1()
    if x is ("3"):
        m1b1()
    if x is ("4"):
        m2b1()
    if x is ("l"):
        left()
    if x is ("r"):
        right()
    if letnum >= 8: # when you have enough letters, move this way and reset
        m1f1()
        sup()
        letnum = 0
        #when letter number has reached 8, shift right, pen down, go up, go up, go up, etc
        #remember to have some way of saying pen up, shift to center, shift down at the end of each set of letter commands
    if linenum >= 3:
        m2b1()
        m2b1()
        m2b1()
        linenum = 0
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
