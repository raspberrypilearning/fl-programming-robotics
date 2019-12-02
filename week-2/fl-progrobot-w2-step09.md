[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Avoiding an obstacle

So far, you have created programs for moving the robot buggy and detecting objects at different distances. Now you are going to combine these two algorithms so that the buggy can autonomously avoid an obstacle.

### Using both the motors and the UDS

To create a program for detecting and navigating around an object, you will need to utilise some of the code you have written so far in this course.

As this program will involve interacting with two pieces of hardware - the motors and the UDS - I'm going to first break my problem down into several parts, which I will pose as questions:

+ What hardware do I need to access within my program and what libraries do these rely on?
+ At what distance is an object too close to the buggy?
+ What should happen if an object is too close to the buggy? 

#### Interacting with the hardware

The quickest way to setup the hardware with the correct GPIO pin numbers and the necessary libraries is by using your previous code to assist you.

**1.** Make a copy of the program you created in the previous step to calculate the distance of an object in front of the UDS. 

**2.** Change the `gpiozero` import statement so that `Robot` is also imported from the GPIO Zero library:

~~~ python
from gpiozero import Robot, InputDevice, OutputDevice
from time import sleep, time
~~~

**3.** Setup the motors as well as the UDS so both pieces of hardware can be communicated with via the GPIO pins on the Raspberry Pi.

~~~ python 
trig = OutputDevice(4)
echo = InputDevice(17)

robin = Robot(left=(8,7), right=(9,10))
~~~

Remember that your GPIO pin numbers for the motors or the UDS may be different to the code above. Check your previous programs that were working and change any of the pin numbers as needed. You may have also renamed the variable `robin` to something else.

**4.** The rest of the program should be the same as before:

~~~ python
sleep(2)

def get_pulse_time():
    trig.on()
   	sleep(0.00001)
	trig.off()

	while echo.is_active == False:
		pulse_start = time()

	while echo.is_active == True:
		pulse_end = time()

	sleep(0.06)

	return pulse_end - pulse_start

def calculate_distance(duration):
	speed = 343
	distance = speed * duration / 2
	return distance

while True:
	duration = get_pulse_time()
	distance = calculate_distance(duration)
	print(distance)
~~~

#### How close is too close?

Currently, the program calculates the distance an object is from the UDS in metres. Next, you need to work out at what distance an object is too close before the buggy responds. I'm going to choose 20cm (or 0.2 metres) as my threshold value for now and I can experiment with this value later.

**5.** Inside the `while True` loop and after `distance` has been calculated, you are going to check if an object is less than 0.2 metres away:

~~~ python
if distance < 0.02:
    print("Too close!")
~~~

### What should the buggy do?

You now have two scenarios to plan for: what should the buggy do if an object is too close to it and what should the buggy do if there isn't an object close by. 

For this program, the buggy should move forward unless an object is too close. If an object is detected as too close, move the buggy left, right or backward to avoid the obstacle in front. 

**6.** I've chosen to move the buggy left if an object is 20cm or less away, else the buggy should move forward. 

~~~ python
if distance < 0.02:
    robin.left()
else:
    robin.forward()
~~~

You could chose another direction to turn once an obstacle is detected instead of left. Experiment with different distance thresholds and see how that affects the buggy.

### Limitations of the program

You may have found that an object which is super close to the UDS returns a much larger distance than expected. This is usually occurs if an object is closer than the minimum distance a UDS can detect accurately - for my UDS that's anything 2mm or less away. Likewise, a UDS will have a maximum range it can measure accurately, which for my UDS is 500cm or half a metre. 

At the moment, this limitation of the sensor isn't going to affect the program massively but be aware of it incase the buggy doesn't behave as intended with really close or distant objects. You could try and find a hack to detect and respond to really close or distant objects.

How well can your buggy avoid an object?

Did you find a work around for an object that was too close for the UDS to measure the distance accurately?

Share your thoughts and code in the comments below.