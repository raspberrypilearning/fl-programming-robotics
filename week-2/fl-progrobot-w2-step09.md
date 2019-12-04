[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Avoiding obstacles autonomously

So far, you have created programs for moving the robot buggy and detecting objects at different distances. Now you are going to create a program for detecting and navigating around objects autonomously.

### Programming both the motors and the UDS

For this program, you will need to bring together some of the code you have written so far in this course to solve a new problem. To begin this process, I am going to consider the different stages of the problem by breaking it down into several parts, which I will pose as questions:

+ What **hardware** does my program need to interact with?
+ What should the buggy do if an object is ***not*** too close to it? 
+ How should the buggy behave when an object ***is*** too close? 

#### Interacting with the hardware

Firstly, I must consider what hardware I am going to be communicating with. The choice of hardware also leads me to consider which programming libraries are required. 

There are two pieces of hardware that this program needs to interact with; the motors for moving the buggy and the UDS for detecting objects. 

One of the libraries I will use is GPIO Zero, from which I will import `Robot` to control the motors, as well as `InputDevice` and `OutputDevice` to communicate with the UDS. 

The other library that the program will rely on is time, which is necessary for determining when the motors or UDS should perform certain actions. From this library I need to import `sleep` and `time`.

**Setting up the new program**

The quickest way to setup the program with the correct GPIO pins for your buggy is to use your previous code.

**1.** Make a copy of the program you created in the previous step to calculate the distance of an object in front of the UDS.

**2.** Change the `gpiozero` import statement so that `Robot` is also imported from the GPIO Zero library:

~~~ python
from gpiozero import Robot, InputDevice, OutputDevice
from time import sleep, time
~~~

**3.** Setup the motors in addition to the UDS so that both pieces of hardware can be communicated with via the GPIO pins on the Raspberry Pi.

~~~ python 
trig = OutputDevice(4)
echo = InputDevice(17)

robin = Robot(left=(8,7), right=(9,10))
~~~

Remember that your GPIO pin numbers for the motors or the UDS may be different to the code above. Check your previous programs that were working and change the pin numbers to reflect the connections on your Raspberry Pi if necessary. You may have also renamed the variable `robin` to something else.

**4.** The rest of the code should be the same as the program in the last step:

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

#### What should the buggy do if there isn't an object nearby?

The robot buggy should move forwards unless it detects an object that is too close. 

Although you could program the buggy to move forwards inside the `while True` loop, this would result in the buggy moving forever unless you turn off the Raspberry Pi. Therefore, I'm going to change the `while` loop to a `for` loop so that the buggy moves forward for a set number of times before stopping the buggy.

**5.** Replace the `while` loop with the following code:

~~~ python 
for i in range(30):
    duration = get_pulse_time()
    distance = calculate_distance(duration)
    print(distance)
    
    robin.forward()

robin.stop()
~~~

The robot buggy will now move forwards 30 times and then the buggy will stop moving before the program ends.

**Remember**: you may have changed the `Robot` variable from `robin` to something else.

#### What should the buggy do if an object is too close?

At the moment, the buggy moves forwards regardless of how close it is to an object. If an object is detected as being within a certain distance of the UDS, then the buggy should move left or right to avoid the obstacle in front.

**How close is too close?**

The program currently calculates the distance an object is from the UDS in metres. You need to specify the threshold value of when an object is too close before the buggy responds. 

The threshold value I'm going to choose is 20cm (0.2 metres) for now; I can experiment with this value later.

**6.** Inside the `for` loop and after `distance` has been calculated, you are going to check if an object is less than 0.2 metres away. Remove the command `robin.forward()` and replace it with:

~~~ python
if distance < 0.2:
    robin.left()
    sleep(0.5)
else:
    robin.forward()

sleep(0.1)
~~~

For this program, I have chosen to move the buggy left if an object is 20cm or less away, otherwise the buggy should move forward. You could chose another direction to move once an obstacle is detected, for example right or backward and then left or right. 

I also instructed the program to wait for 0.5 seconds once the threshold value is met so that the buggy has enough time to move out of the way - again, the value specified can be changed.

The last `sleep` ensures the program waits for 0.1 seconds before attempting to detect more objects so the UDS has time to settle.

Your final code for the end of the program should be:

~~~ python
for i in range(30):
    duration = get_pulse_time()
    distance = calculate_distance(duration)
    print(distance)
    
    if distance < 0.2:
        robin.left()
        sleep(0.5)
    else:
        robin.forward()

    sleep(0.1)

robin.stop()
~~~

### Test the program

Try running the program whilst the buggy is on a suitable surface. 

If the buggy is not behaving as expected, first check that all the connections to the GPIO pins are correct before trying the code again. It can also be beneficial to run an earlier program you know was working to test whether the motors and UDS are still working as expected.

Leave a comment below if you are having issues with the buggy or if you found a solution to a problem you faced.