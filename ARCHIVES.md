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
#For the servo functions, there is an s in front of the direction that it goes in
#The motor functions do not have an initial letter, just the direction the plate will go in
#If there are two directions, i.e. upright, or downleft, it is a diagonal movement in that direction
#The number after the motor function indicates how much of a turn the motors will do, but it is one/number turn
#For example
# take the below function, no initial s, so it's for the motor, and it will move the plate right
def right1(): # the 1 indicates a fullturn
    for step in range (FULLTURN):
        motor2.onestep(style=stepper.DOUBLE) #both motors are moving forward, creating right motion in corexy system
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def right2 (): #the 2 here means a half turn
    for step in range (HALFTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def right4 (): #4 is for quarter turn
    for step in range (QTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def right8 (): #and so on and so forth
    for step in range (ETURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)


def left1 ():
    for step in range (FULLTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def left2 ():
    for step in range (HALFTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def left4 ():
    for step in range (QTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def left8 ():
    for step in range (ETURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def up1 ():
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

def up8 ():
    for step in range (ETURN):
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

def down8 ():
    for step in range (ETURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)

def upright1 (): #getting fancy with diagonals
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

def upright8 ():
    for step in range(ETURN):
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

def downleft8 ():
    for step in range(ETURN):
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

def upleft8 ():
    for step in range(ETURN):
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

def downright8 ():
    for step in range(ETURN):
        motor2.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def sup (): #only two servo functions to lift the pen and put the pen down
    my_servo.angle = 50

def sdown ():
    my_servo.angle = 46


while True:
    x = input("Enter command: ") #keyboard setup stuff, x is the variable that holds letters
    print(letnum)
    if x is ("k"):
        sdown()
        downright2()
        up4()
        sup()
        letnum = letnum + 1
    if x is ("w"):
        up2()
    if x is ("a"):
        left2()
    if x is ("s"):
        down2()
    if x is ("d"):
        right2()
    if x is ("m"):
        sdown()
    if x is ("n"):
        sup()

#This is a simplified version of the code to write the language, the code for the language is unfinished as of 5/30/2024
#which is when I am writing this note.

```

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

def right1():
    for step in range (FULLTURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(style=stepper.DOUBLE)
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

def right8 ():
    for step in range (ETURN):
        motor2.onestep(style=stepper.DOUBLE)
        motor1.onestep(style=stepper.DOUBLE)
        time.sleep(DELAY)


def left1 ():
    for step in range (FULLTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def left2 ():
    for step in range (HALFTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def left4 ():
    for step in range (QTURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def left8 ():
    for step in range (ETURN):
        motor2.onestep(direction=stepper.BACKWARD)
        motor1.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def up1 ():
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

def up8 ():
    for step in range (ETURN):
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

def down8 ():
    for step in range (ETURN):
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

def upright8 ():
    for step in range(ETURN):
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

def downleft8 ():
    for step in range(ETURN):
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

def upleft8 ():
    for step in range(ETURN):
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

def downright8 ():
    for step in range(ETURN):
        motor2.onestep(direction=stepper.BACKWARD)
        time.sleep(DELAY)

def sup ():
    my_servo.angle = 50

def sdown ():
    my_servo.angle = 46


while True:
    x = input("Enter command: ") #keyboard setup stuff, x is the variable that holds letters
    print(letnum)
    if x is ("k"):
        sup()
        left4()
        sdown()
        downright2()
        up8()
        sup()
        left4()
        down4()
        letnum = letnum + 1
    if x is ("g"):
        sup()
        left4()
        sdown()
        downright2()
        sup()
        upleft2()
        down8()
        sdown()
        downright2()
        up4()
        sup()
        left2()
        down4()
        letnum = letnum + 1
    if x is ("s"):
        sup()
        left4()
        sdown()
        down4()
        upright2()
        sup()
        left2()
        down4()
    if x is ("z"):
        sup()
        left4()
        sdown()
```
