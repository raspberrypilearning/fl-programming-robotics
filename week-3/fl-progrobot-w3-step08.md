[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Program a line following algorithm

So far this week, you have connected 2 line sensors to the robot buggy and tested that each sensor detects the difference between a white surface and a black line. Now you are going to code, test, and refine an algorithm so that your buggy is able to follow a line.

### Writing a basic line following algorithm

To begin with, you are going to write a basic line following algorithm to test that your robot is working.

#### Setting up the motors and line sensors

**Note:** In this example, the motor controller board is connected so that the left motor is on pins **GPIO 7** and **GPIO 8**, and the right motor is on pins **GPIO 9** and **GPIO 10**. The left line sensor is on pin **GPIO 19**, and the right line sensor is on pin **GPIO 26**. 

**1.** First, create a new Python 3 file.

**2.** You need to start the program by setting up the motor controller board and line sensors using `gpiozero`. 

~~~ python
from gpiozero import Robot, LineSensor
from time import sleep

robin = Robot(left=(8, 7), right=(9, 10))
left_sensor = LineSensor(19)
right_sensor= LineSensor(26)
~~~

Remember, I changed the GPIO pin order for the left motor in my original build but yours might be different. Use your previous working code to make sure you have defined the correct GPIO pins for the motors. You may have also renamed the variable `robin` to something else.

Check your setup for the line sensors as you may have chosen different GPIO pins for the left and right line sensors, or the pin numbers could be swapped around. 

#### Programming the buggy behaviour based on the line

The algorithm should perform the four following tasks based on where the line is:

+ If there’s a line under the left sensor, turn left
+ If there’s a line under the right sensor, turn right
+ If there’s no line under the left sensor, drive forwards
+ If there’s no line under the right sensor, drive forwards

**3.** You are going to use two commands from `LineSensor` to begin with; `when_line` and `when_no_line`. Each sensor will call a function depending on whether or not a line has been detected:

~~~ python
left_sensor.when_line = robin.left
right_sensor.when_line = robin.right
left_sensor.when_no_line = robin.forward
right_sensor.when_no_line = robin.forward
~~~

By telling the robot to go forward when no line has been detected, but to turn if a line is detected, you can produce basic line following behaviour.

Each of the `when_line` and `when_no_line` commands will continue to run, even after you close the program. 

To make sure that the robot doesn’t keep running forever, and to close all the components connections cleanly, you can optionally add in these lines to the end of your program as well:

~~~ python
sleep(20)

robin.stop()
robin.close()
left_sensor.close()
right_sensor.close()
~~~

After 20 seconds, the motors will be instructed to stop moving. Then the `close()` command will ensure that the motors and line sensors are shut down completely. 

#### Testing the basic algorithm

**4.** Try running the program once your robot is placed directly over the line of your track.

Don’t worry if you’re robot moves off the line a bit. Just observe if it attempts to stay on the line. Here’s an example of a robot running on a basic track with this algorithm.

![Video-gif of the robot wiggling side to side as it follows a basic track](images/3_8-basic-line-following-robot)
