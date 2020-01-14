[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Program a line following algorithm

Now that you have attached the line sensors, you can develop a basic line following algorithm based on the readings of the line sensors. First, let's set up the program before moving on to the algorithm. 

### Setting up the motors and line sensors

**1.** Create a new Python 3 file.

**2.** Begin the program by setting up the motor controller board and line sensors using the `gpiozero` library.

~~~ python
from gpiozero import Robot, LineSensor
from time import sleep

robin = Robot(left=(8, 7), right=(9, 10))
left_sensor = LineSensor(19)
right_sensor= LineSensor(26)
~~~

Don’t forget to adjust the pin numbers if you’ve used different GPIO pins for the motors or line sensors.

### Describing the algorithm

The line sensors have 2 states; the line **is** detected or the line **is not** detected. The current state of each sensor will help to define the rules of your algorithm.

Start by considering what the robot buggy should do when neither of the sensors detect the line. If the line is in the centre of the robot, both line sensors will return a 0 from their digital pins as they are over the white background. Therefore, the robot should move forwards.

Think about the other factors that make up the line following algorithm: 

+ **What is the initial position of the robot in relation to the line?**
+ **How should the robot react when the left sensor is over the line?**
+ **What about when the right sensor detects the line?**
+ **How have you previously programmed the robot to move using the `gpiozero` library?**

![](images/3_4_Two_Sensors_Anim.gif)

### Rules of the algorithm

The actions that the robot needs to take depending on the readings from the line sensors are as follows:

+ If there’s a line under the left sensor, turn left
+ If there’s a line under the right sensor, turn right
+ If there’s no line under the left sensor and the right sensor, drive forwards

### Programming the algorithm

To detect the state of each sensor, you are going to use two events from `LineSensor`, which is part of the `gpiozero` library. 

An event is an action that occurs based on user interaction or a change in behaviour, such as a button being pressed. 

Synchronous

When an event is activated...

These events are called `when_line` and `when_no_line`.

**3.** Within the Python file you set up, program your robot to move in a certain direction based on the rules of the algorithm.

~~~ python
left_sensor.when_line = robin.left
right_sensor.when_line = robin.right
left_sensor.when_no_line = robin.forward
right_sensor.when_no_line = robin.forward
~~~

Notice that the functions to move the robot do not end in brackets; this is due to how the events are defined in `LineSensor` and means you can't pass any values inside brackets, such as the speed of the motors.

### Ensuring the program doesn't run forever

Currently, the motors will continue to run even after you close the program. If you ran the program at the moment, you would probably need to turn off the Raspberry Pi to stop the robot buggy from moving.

**4.** To make sure that the robot doesn’t keep running forever, and to close all the component's connections cleanly, add in the following lines of code to the end of your program:

~~~ python
sleep(10)

robin.stop()
robin.close()
left_sensor.close()
right_sensor.close()
~~~

After 10 seconds, the motors will be instructed to stop moving with the `stop()` command. Then the `close()` command will ensure that the motors and line sensors are shut down completely.

You can change the number of seconds to a different value if you want to test the robot for shorter or longer periods of time.

### Testing the algorithm

<!-- Find out why and potentially modify explanation -->
Before you run the program, be aware that the `when_line` and `when_no_line` events might not initially activate until after one of them changes state. Once you run the program, you will need to move the robot so one of the sensors changes from over a line to not over a line or vice versa. Or you can add the line `robin.forward()` just before these events.

**5.** Try running the program once your robot is placed directly over the line of your track.

Here is an example of a robot running on a basic track with this algorithm:

![Video-gif of the robot wiggling side to side as it follows a basic track](images/3_8-basic-line-following-robot)

Don’t worry if your robot moves off the line a bit. Just observe if it attempts to stay on the line. If it doesn't stay on the line, check that the algorithm and the GPIO pin numbers you have specified in the program are correct. You may also need to test that the line sensors are accurately detecting the difference between the white surface and black line, using the instructions earlier in the week.
