# Engr3robotarmLG

### PROJECT DESCRIPTION
This project is a robot that writes out letters in a created language called Angarkase according to keyboard inputs put in by a person. You will be able to input a letter, and a small plate
with a piece of paper will move with a pen over it, which will be attached to a servo in order to lift and put down the pen. 

### CODE
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

pwm = pwmio.PWMOut(board.D7, duty_cycle=2 ** 15, frequency=50) #servo setup stuff

my_servo = servo.Servo(pwm) #naming the servo

#FUNCTION GUIDE:
#first letter + number indicates type of motor and motor number
#s is servo, m1 is motor 1 and m2 is motor 2
#pos is position followed by position number
def m1pos1 ():
    for step in range(FULLTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m1pos2 ():
    for step in range(HALFTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m1pos3 ():
    for step in range (QTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m1pos4 ():
    for step in range(ETURN):
        motor1.onestep(direction=stepper.DOUBLE)
        time.sleep(DELAY)

def m1pos5 ():
    for step in range (FULLTURN):
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def m2pos1 ():
    for step in range(FULLTURN):
        motor2.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m2pos2 ():
    for step in range(HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m2pos3 ():
    for step in range (QTURN):
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def m2pos4 ():
    for step in range(ETURN):
        motor1.onestep(direction=stepper.DOUBLE)
        time.sleep(DELAY)

def m2pos5 ():
    for step in range (FULLTURN):
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def sUp ():
    my_servo.angle = 120

def sDown ():
    my_servo.angle = 100


while True:
    x = input("Enter command: ") #keyboard setup stuff, x is the variable that holds letters
    print(letnum)
    print(linenum)
    if x is ("k"): #if you input the letter in the "", the stepper will do these function
        sUp()
        m1pos1()
        time.sleep(.2)
        sDown()
        m1pos2()
        letnum = letnum + 1 #uptick variable by 1
    if x is ("g"):
        sUp()
        m1pos4()
        letnum = letnum + 1
    if x is ("t"):
        m1pos5()
        time.sleep(.5)
        sDown()
        m1pos3()
        letnum = letnum + 1
    if x is ("d"):
        m1pos4()
        time.sleep(.5)
        sDown()
        m1pos5()
        letnum = letnum + 1
    if letnum >= 8: # when you have enough letters, move this way and reset
        m1pos1()
        sUp()
        letnum = 0
        linenum = linenum + 1 #when letter number has reached a certain point

        #when letter number has reached 8, shift right, pen down, go up, go up, go up, etc
        #remember to have some way of saying pen up, shift to center, shift down at the end of each set of letter commands

```

### ONSHAPE LINK
(https://cvilleschools.onshape.com/documents/d0332011792ff0881e4ecb2d/w/f60ced9a74de595b67e1cf04/e/22963176449209f64e9ac10e?renderMode=0&uiState=66314a3d5f4708045409fd3d)
