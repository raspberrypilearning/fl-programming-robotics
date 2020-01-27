[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Avoiding obstacles autonomously

So far, you have created programs for moving the robot buggy and detecting objects at different distances. Now you are going to create a program for detecting and navigating around objects autonomously.

### Programming both the motors and the UDS

For this program, you will need to bring together some of the code you have written in during the course to solve a new problem. 

To help you begin this process, consider the different stages of the problem by breaking it down into several parts, which I will pose as questions:

+ What **components** does your program need to interact with?
+ What should the robot do if an object is ***not*** too close to it?
+ How should the robot behave when an object ***is*** too close?

#### Interacting with the hardware

The first question to think about is what components does your robot need to communicate with so it can sense objects and move accordingly?

One of the components you will need to use is the UDS for detecting objects in front of the robot. 

**1.** Make a copy of your program from the previous step which calculates the distance of objects using the UDS. 

The other components that your program needs to interact with are the motors. 

**2.** Change the first line of code so that `Robot` is also imported from the `gpiozero` library.

~~~ python
from gpiozero import Robot, InputDevice, OutputDevice
~~~

You will also need to setup the `Robot` with the GPIO pins for the `left` and `right` commands. 

**3.**



**3.** After the two import statements for the 


You can use one of your working programs from week 1 to check that the GPIO pins of your motors are set correctly. 


<!-- Copy Robot explanation from week 1 -->


**3.** Setup the motors in addition to the UDS so that both pieces of hardware can be communicated with via the GPIO pins on the Raspberry Pi.

~~~ python
trig = OutputDevice(4)
echo = InputDevice(17)

robin = Robot(left=(8,7), right=(9,10))
~~~

Remember that your GPIO pin numbers for the `left` and `right` motors or the `trig` and `echo` pins of the UDS may be different to the code above. Check the previous programs that you got working and change the pin numbers to reflect the connections on your Raspberry Pi if necessary. You may have also renamed the variable `robin` to something else.

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

#### The default option for the robot

The robot should, by default, move forwards unless it detects an object that is too close.

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

At the moment, the robot moves forwards regardless of how close it is to an object. If an object is detected as being within a certain distance of the UDS, then the robot should turn left or right to avoid the obstacle in front.

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

For this program, I have chosen to turn the robot left if an object is 20cm or less away, otherwise the robot should move forward. 

I also instructed the program to wait for 0.5 seconds once the threshold value is met so that the buggy has enough time to move out of the way.

The last `sleep` ensures the program waits for 0.1 seconds before attempting to detect more objects, allowing the UDS time to settle.

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

### Testing the obstacle avoidance

Try running the program whilst the robot is on a suitable surface.

If the buggy is not behaving as expected, first check that all the connections to the GPIO pins are correct before trying the code again. It may also be beneficial to run an earlier program you know was working to test whether the motors and UDS are still working as expected.

How effective is your robot at avoiding objects? 

In the next step, you will look at some ways to improve your program. Can you think of any modifications that might help?

Leave a comment below if you are having issues with the obstacle avoidance program, or if you found a solution to a problem you faced.
