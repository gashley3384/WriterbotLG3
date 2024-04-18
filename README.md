# Engr3robotarmLG
For making the robot arm

```python
import board
import time
import digitalio
from adafruit_motor import stepper 
from adafruit_motor import servo
import pwmio

DELAY = 0.01
FULLTURN = 200 #Stepper has up to 200 steps, few variable
HALFTURN = 100
QTURN = 50
ETURN = 25
letnum = 0  #number of letter, allows for going to the next line

coils1 = (
    digitalio.DigitalInOut(board.D9),  # A1
    digitalio.DigitalInOut(board.D10), # A2
    digitalio.DigitalInOut(board.D11), # B1
    digitalio.DigitalInOut(board.D12), # B2
) # we gotta set up those coils

for coils in coils1:
    coils.direction = digitalio.Direction.OUTPUT #motor is the output


motor1 = stepper.StepperMotor(coils1[0], coils1[1], coils1[2], coils1[3], microsteps=None) #motor setup stuff

pwm = pwmio.PWMOut(board.D7, duty_cycle=2 ** 15, frequency=50) #servo setup stuff

my_servo = servo.Servo(pwm) #naming the servo

while True:
    x = input("Enter command: ") #keyboard setup stuff, x is the variable that holds letters
    print(letnum)
    if x is ("f"): #if you input f, the stepper will do this and the servo will do this
        my_servo.angle = 160
        for step in range(QTURN):
            motor1.onestep(style=stepper.DOUBLE)
            time.sleep(DELAY)
        letnum = letnum + 1 #uptick variable by 1
    if x is ("v"):
        my_servo.angle = 180
        for step in range(HALFTURN):
            motor1.onestep(direction=stepper.BACKWARD)
            time.sleep(DELAY)
        letnum = letnum + 1
    if letnum >= 8: # when you have enough letters, move this way and reset
        my_servo.angle = 90
        for step in range(FULLTURN):
            motor1.onestep(direction=stepper.BACKWARD)
            time.sleep(DELAY)
        letnum = 0
```
