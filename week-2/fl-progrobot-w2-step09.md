[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Avoiding obstacles autonomously

So far, you have created programs for moving the robot buggy and detecting objects at different distances. Now you are going to create a program for detecting and navigating around objects autonomously.

### Programming both the motors and the UDS

For this program, you will need to bring together some of the code you have written during the course to solve a new problem. 

To help you begin this process, consider the different parts of the problem:

+ What **components** does your program need to interact with?
+ What should the robot do if an object is ***not*** too close to it?
+ How should the robot behave when an object ***is*** too close?

#### Interacting with the hardware

The first thing to think about is the components your robot needs to communicate with so it can sense objects (the UDS) and move accordingly (the motors).

To speed up this process, make a copy of your program from the previous step which calculates the distance of objects from the UDS. Then you will modify the code to include the motors.

**1.** Make a copy of your program from the previous step. 

**2.** Change the first line of code so that `Robot` is also imported from the `gpiozero` library to control the motors.

~~~ python
from gpiozero import Robot, InputDevice, OutputDevice
~~~

**3.** After the `trig` and `echo` variables have been initialised, define the `Robot` using the GPIO pins for your `left` and `right` motors. 

~~~ python
robin = Robot(left=(8,7), right=(9,10))
~~~

You can use one of your working programs from week 1 to check that the GPIO pins of your motors are set correctly, as they may be different to the ones I've used above.

#### Setting up a timer

Next you are going to create a timer so that your robot doesn't run forever, which is especially useful during the testing phases. 

**4.** Add in these three variables just after you have initialised `Robot`:

~~~ python 
duration = 10
end_time = time() + duration
running = True
~~~

The value of `duration` is the number of seconds that the timer will run for. Calculate `end_time` by adding `duration` to the current time using the `time()` function. 

You will use the `running` variable later to specify when the program - and the robot - should stop running.

#### Your code so far

At the moment, your program should look similar to this:

~~~ python
from gpiozero import Robot, InputDevice, OutputDevice
from time import sleep, time

trig = OutputDevice(4)
echo = InputDevice(17)

robin = Robot(left=(8,7), right=(9,10))

duration = 10
end_time = time() + duration
running = True

sleep(2)

def get_pulse_time():
    trig.on()
    sleep(0.00001)
    trig.off()

    while echo.is_active == False:
        pulse_start = time()

    while echo.is_active == True:
        pulse_end = time()

    return pulse_end - pulse_start

def calculate_distance(duration):
    speed = 343
    distance = speed * duration / 2
    return distance

while True:
    duration = get_pulse_time()
    distance = calculate_distance(duration)

    sleep(0.06)
    print(distance)
~~~

The last changes you are going to make are going to all be with the `while` loop. 

#### How should the robot behave?

The robot should, by default, move forwards unless it detects an object that is too close. If an object is detected within a certain distance of the UDS, then the robot should turn left or right to avoid the obstacle in front.

*How close is too close?*

The program currently calculates the distance an object is from the UDS in metres. You need to specify the threshold value (in metres) of when an object is too close to the robot.

For now, the threshold value I'm going to choose is 20cm (0.2 metres); you can experiment with this value later.

**5.** Inside the `while` loop and before the `sleep(0.06)` command, check if an object is less than 0.2 metres away. If the distance is below the threshold value then program the robot left for half a second, else move forward. 

~~~ python
if distance < 0.2:
    robin.left()
    sleep(0.5)
else:
    robin.forward()
~~~

Using a sleep command here inside the if statement means that the robot will continue to turn left for a certain amount of time before checking for more obstructions. Hopefully, this will allow your robot enough time to turn clear of the object that was detected.

**6.** To stop the program from running forever, add in the following code inside the `while` loop after the `sleep(0.06)` command.

~~~ python
    if time() >= end_time:
        running = False
        robin.stop()
~~~

This checks if the current time is more than or equal to the `end_time` value specified at the start of the program. If so, change the value of `running` to `False` and then stop the motors of the robot.

**7.** Modify the `while` loop condition so that it stops repeating once `running` is set to `False`.

Change the condition from

~~~ python
while True:
~~~
 
to

~~~ python
while running:
~~~

Your final code for the `while` loop should be:

~~~ python
while running:
    duration = get_pulse_time()
    distance = calculate_distance(duration)

    if distance < 0.2:
        robin.left()
        sleep(0.5)
    else:
        robin.forward()

    sleep(0.06)

    if time() >= end_time:
        running = False
        robin.stop()
~~~

### Testing the program

Try running the program whilst the robot is on a suitable surface.

If the buggy is not behaving as expected, check that all the connections to the GPIO pins are correct before trying the code again. 

It may also be beneficial to run an earlier program you know was working to test whether the motors and UDS are still working as expected.

**How effective is your robot at avoiding objects?**

**Can you think of any modifications that might help?**

Share your answers or if you are having any issues in the comments below.

In the next step, you will look at some ways to improve your program.
