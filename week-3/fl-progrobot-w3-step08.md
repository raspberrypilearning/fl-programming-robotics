[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Program a line following algorithm

The line sensors you have attached to your robot buggy should be able to detect the difference between the white surface and black line of your track. You are now going to use the information from both the sensors to program how the buggy should behave so it can follow a line.

### The algorithm

To develop a basic line following algorithm, you need to consider how the robot should act depending on the readings of the line sensors.

The sensors have 2 states; the line **is** detected or the line **is not** detected. The current state of each sensor will help to define the rules of your algorithm.

Let's start by considering what the robot buggy should do when neither of the sensors detect the line. If the line is in the centre of the robot then both sensors will return a 0 from their digital pins, as they are both over the white background and the line has not been detected. Therefore, the robot should move forwards.

Think about the other factors that make up the line following algorithm. **How should the robot react when the left sensor is over the line? What about when the right sensor detects the line? How have you previously programmed the robot to move using the `gpiozero` library?**

![](images/3_4_Two_Sensors_Anim.gif)

#### The four rules of the algorithm

For my algorithm, I am going to define four courses of action that the robot can take depending on where the line is:

+ If there’s a line under the left sensor, turn left
+ If there’s a line under the right sensor, turn right
+ If there’s no line under the left sensor, drive forwards
+ If there’s no line under the right sensor, drive forwards

I will revisit these rules when I come to code a solution to the line following algorithm, but first you need to setup the line sensors and motors in a new Python program.

### Programming the algorithm

#### Setting up the motors and line sensors

**1.** Create a new Python 3 file.

**2.** Start the program by setting up the motor controller board and line sensors using the `gpiozero` library.

~~~ python
from gpiozero import Robot, LineSensor
from time import sleep

robin = Robot(left=(8, 7), right=(9, 10))
left_sensor = LineSensor(19)
right_sensor= LineSensor(26)
~~~

**Note:** In this example, the left line sensor is connected to pin **GPIO 19** on the Raspberry Pi and the right line sensor is on pin **GPIO 26**. Check your build as you may have chosen different GPIO pins for the left and right line sensors, or the pin numbers could be swapped around.

Also, you may have used different GPIO pins for the `left` and `right` motors, and perhaps a different variable name to `robin`. Use your previous working code to make sure you have defined the correct GPIO pins for your motors.

#### Reading the sensors

You are going to incorporate the four rules of the algorithm, which I specified earlier in this article, to perform certain actions depending on the readings from the line sensors.  

To detect the state of each sensor, you are going to use two events from the `LineSensor` that's part of the `gpiozero` library. These events are called `when_line` and `when_no_line`.

**3.** Call a function to move the robot in a certain direction depending on whether the left and right sensor has detected a line or not:

~~~ python
left_sensor.when_line = robin.left
right_sensor.when_line = robin.right
left_sensor.when_no_line = robin.forward
right_sensor.when_no_line = robin.forward
~~~

By telling the robot to go forward when no line has been detected, but to turn if a line is detected, you can produce basic line following behaviour.

Notice that the functions to move the robot do not end in brackets; this is due to how the events are defined in `LineSensor`.

#### Ensuring the program doesn't run forever

Each of the `when_line` and `when_no_line` events will continue to run, even after you close the program. If you ran the program at the moment, you would probably need to turn off the Raspberry Pi to stop the robot buggy from moving.

<!-- The values of the devices will stay at whatever value they have been set as.  -->

**4.** To make sure that the robot doesn’t keep running forever, and to close all the components connections cleanly, add in the following lines of code to the end of your program:

~~~ python
sleep(20)

robin.stop()
robin.close()
left_sensor.close()
right_sensor.close()
~~~

After 20 seconds, the motors will be instructed to stop moving with the `stop()` command. Then the `close()` command will ensure that the motors and line sensors are shut down completely.

You can change the number of seconds to a different value if you want to test the robot for shorter or longer periods of time.

#### Testing the basic algorithm

<!-- Find out why and modify explanation -->
Before you run the program, be aware that the `when_line` and `when_no_line` events won't initially activate until after one of them changes state. Once you run the program, you will need to move the robot so one of the sensors changes from over a line to not over a line or vice versa. Or you can add the line `robin.forward()` just before these events.

**5.** Try running the program once your robot is placed directly over the line of your track.

Here is an example of a robot running on a basic track with this algorithm:

![Video-gif of the robot wiggling side to side as it follows a basic track](images/3_8-basic-line-following-robot)

Don’t worry if your robot moves off the line a bit. Just observe if it attempts to stay on the line. If it doesn't stay on the line, check that the algorithm and the GPIO pin numbers you have specified in the program are correct. You may also need to test that the line sensors are accurately detecting the difference between the white surface and black line, using the instructions earlier in the week.
