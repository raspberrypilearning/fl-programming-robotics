[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Designing a more complex algorithm

The previous line following algorithm is okay, but the robot can move side to side quite a lot as it tries to keep track of the line. This is partly down to the speed of the robot; slowing the robot down a bit means that the left and right turns are smaller and therefore more gradual.

However, the `when_line` and `when_no_line` events don't allow you to modify the robot's speed or other properties. 

In the previous algorithm, the events `when_line` and `when_no_line` don't allow you to modify the robot's speed or other properties.


### Setting up the program

**1.** In a new Python 3 file, add these lines of code:

~~~ python
from gpiozero import Robot, LineSensor
from time import sleep, time

robin = Robot(left=(8, 7), right=(9, 10))
left_sensor = LineSensor(19)
right_sensor= LineSensor(26)
~~~

Remember to adjust the pin numbers if you’ve used different GPIO pins. 

The only difference from the set up of the previous program so far is that you are also importing `time` from the `time` library. This will be used to create a timer so the program does not run forever. 

**2.** Create variables that will be used to control the speed of the motors and the duration of time that the program will run.

~~~ python 
speed = 0.75

duration = 20
end_time = time() + duration

running = True
~~~

The multiplier for `speed` usually needs to be above 0.6 otherwise the motors do not have enough momentum to turn on a solid surface. The maximum value for `speed` is 1.

`duration` is how many seconds the program will run for. By adding this value to the current `time()` you can calculate the `end_time` for stopping the program.

You will use the `running` variable to specify when the program should stop running.

### Planning a better algorithm

In the previous algorithm, the events `when_line` and `when_no_line` don't allow you to modify the robot's speed or other properties.

To have more control over the robot's movement, you can read the values of the line sensors and use these to instruct which way each of the robot's left and right motors should turn, and by how much.



When a line sensor is above a line, it outputs a `1`. When it’s off a line, it outputs a `0`.

The motors work slightly differently though as they have a range from `-1` to `1`; positive values tell the motor to run forwards and negative values run the motor in reverse. 


Let’s have a look at an algorithm that takes into account the position of the robot, the states of the lines sensors, and the actions required of the motors.




The motors work slightly differently though: the robot, whenever it receives a 1 signal to the right motor, drives that motor forwards. When it receives a -1, it drives the motor backwards.




Let's see how you can set the value of each of the motors based on the readings from the line sensors.

### Rules of the new algorithm


The motors work on a range from `-1` to `1`; positive values tell the motor to run forwards and negative values run the motor in reverse. 

To turn left


If the robot is perfectly over the line, both line sensors are off the line (outputting `0`). In this case, the robot should move forward, so both motors should receive the same positive value.

If the robot has drifted to one side, the sensor on the opposite side will move over the line and so will output `1`. For example if the robot has drifted left, the right sensor will read `1`. To turn right, the right motor should run backwards (a negative signal is needed), while the left motor continues to run forwards.
+ If the robot drifed right, the opposite would be true.



Remember that the line sensors output `0` if it is over a white background and `1` if it 



#### Using the sensor readings to set the motor values

Your next step is to send a signal to the motors:

+ If both sensors output `0`, then both motors should receive `1`
+ If the right sensor outputs `1`, then the left motor should receive `-1` and the right motor `1`
+ If the left sensor outputs `1`, then the left motor should receive `1` and the right motor `-1`

![Picture of a table showing the robot directions based on the left line sensor and right line sensor readings](images/3_9-table-sensor-values.jpeg)

*Why do you think there is not a rule for both the sensors outputting a `1` simultaneously?*



+ If the robot is perfectly over the line, both line sensors are off the line (outputting `0`). The robot should continue going forward, so both motors should receive the same positive value.

+ If the robot has drifted to one side, the sensor on the opposite side will move over the line and so will output `1`. This means that:
    + if the robot has drifted left, the right sensor will read `1`. To turn right, the right motor should run backwards (a negative signal is needed), while the left motor continues to run forwards.
    + if the robot drifted right, the opposite would be true.






#### Using the sensor readings to set the motor values

Your next step is to send a signal to the motors:

+ If both sensors output `0`, then both motors should receive `1`
+ If the right sensor outputs `1`, then the left motor should receive `-1` and the right motor `1`
+ If the left sensor outputs `1`, then the left motor should receive `1` and the right motor `-1`

To turn left, the left motor needs a negative value and the right motor needs a positive value.



### Programming the algorithm

**3.** To start applying these rules, the code needs to repeatedly read the outputs of the line sensors, in a loop:

~~~ python 
while running:
    left_detect  = int(left_sensor.value)
    right_detect = int(right_sensor.value)
    
	print (left_detect, right_detect)
~~~

**4.** If you run the program now, you should see the binary output from the sensors, similar to the video below:

![Video-gif of the robot sensors being moved slowly over and off the line with a shot of the line sensor output values changing on the screen changing whenever the robot is moved](images/3_9-binary-output-line-sensors)

**5.** Inside the `while` loop, use conditional statements to specify the direction of each motor depending on the line sensor readings:

~~~ python
while running:
    left_detect  = int(left_sensor.value)
    right_detect = int(right_sensor.value)
    
    if left_detect == 0 and right_detect == 0:
        left_mot = 1
        right_mot = 1
    elif left_detect == 1:
        left_mot = -1
        right_mot = 1
    elif right_detect == 1:
        left_mot = 1
        right_mot = -1

	print (left_mot, right_mot)    
~~~

**6.** Run your code and test that the program outputs the correct motor values when you move the robot over the line.

![Video-gif of the robot sensors being moved slowly over and off the line with a shot of the motor output values changing on the screen changing whenever the robot is moved](images/3_9-binary-output-motors)

**7.** Inside the loop, remove the `print` statement and replace it with:

~~~ python
    robin.left_motor.value = left_mot * speed
    robin.right_motor.value = right_mot * speed
~~~

The value for each motor will be modified by the `speed` multiplier to slow down the robot. 

Make sure you remove any `print` statements within the loop otherwise this will slow down the response time and the robot may "overshoot" the line.

**8.** To stop the `while` loop from running forever, and to close all the component's connections cleanly, add this code inside the loop:

~~~ python
    if time() >= end_time:
        running = False
        robin.stop()
        robin.close()
        left_sensor.close()
        right_sensor.close()
~~~

**9.** Now run your code and test your robot over a track.
