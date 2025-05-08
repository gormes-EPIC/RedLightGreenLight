
# Lab 8: Red Light, Green Light

## Materials

- 1 red and 1 green 5mm LED
- 2 65 Ω (Ohm) resistors or greater
- 1 1k resistor and 1 2k resistor
- 12 male-to-male jumper wires
- HC-SRO4(make sure it has 4 pins!)

## Part 1: Set Up Your HC-SRO4

1. Wire your HC-SRO4 using this tutorial: [Distance Sensor Tutorial](https://pimylifeup.com/raspberry-pi-distance-sensor/). Follow the diagram exactly. Use pin 4 for the Trigger and pin 17 for the Echo.
2. Use the following starter code to test your wiring. It should print the distance every second. 
```python
#!/usr/bin/python
import RPi.GPIO as GPIO
import time
from datetime import datetime

print("time,cm")
while True: 
    try:
        GPIO.setmode(GPIO.BOARD)

        PIN_TRIGGER = 7
        PIN_ECHO = 11

        GPIO.setup(PIN_TRIGGER, GPIO.OUT)
        GPIO.setup(PIN_ECHO, GPIO.IN)

        GPIO.output(PIN_TRIGGER, GPIO.LOW)

        time.sleep(1)
        current_time = datetime.now()

        GPIO.output(PIN_TRIGGER, GPIO.HIGH)

        time.sleep(0.00001)

        GPIO.output(PIN_TRIGGER, GPIO.LOW)

        while GPIO.input(PIN_ECHO)==0:
                pulse_start_time = time.time()
        while GPIO.input(PIN_ECHO)==1:
                pulse_end_time = time.time()

        pulse_duration = pulse_end_time - pulse_start_time
        distance = round(pulse_duration * 17150, 2)

        # Print time and distance in centimeters
        dt = current_time.strftime("%H:%M:%S")
        print (f"{dt},{distance}")

    finally:
        GPIO.cleanup()
```

## Part 2: Add Indicator Lights 

1. Wire both your LEDs on individual pins.
2. Modify your program so the green light lights up when the target is moving >= 1cm/second and the red light lights up when the target is not moving(< 1cm/second). You will need to use `BOARD` numbering to access your pins instead of `BCM` like usual. If you have having trouble with this, please ask for help! 

- [ ] Upload your program and video of your functioning code to your repository. 

## Part 3: Measure Shapes

1. Using the box in class, take distance readings of the secret shape and create a data table with your findings. 
2. Using your data table and your knowledge of geometry identify the shape. On graph paper, draw your shape and calculate its area. 

- [ ] Upload your data table, graph, and area calculation to GitHub
## Deliverables

- Make sure all the deliverables above are  uploaded to the repository
- Answer the following questions:
	1. How does the HC-SR04 sensor calculate distance?
	2. Why is it important to clean up GPIO pins with GPIO.cleanup() at the end of the program?
	3. How did you calculate whether the object was moving ≥ 1 cm/second? 
	4. If your sensor gives you a series of distance readings over time, how can you calculate speed?
	5. How did your data help you identify the shape in Part 3?
## Rubric 

- 6 points - All required items are present.    
- 5 points - Task was completed, but supplementary materials are weak or missing.    
    - Code is complete, but poorly communicates necessary information
- 4 points - Task was attempted, but is missing major components.    
    - Missing comments, videos/photos, or reflection questions  
- 3 points - Did not attempt or student should reattempt.  
    - Inappropriate use of AI tools.
