[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Improving the line following

The previous line following program is okay, but the robot can move side to side quite a lot as it follows the line. To make the robot's movement more elegant you can slow down the speed of the robot, making the turns smaller and more gradual.

However, the `when_line` and `when_no_line` events don't allow you to modify the robot's default speed. To have more control over the robot, you can adapt your program so that it takes into account the states of the line sensors, and uses these to choose the actions required of the motors.

### Setting up the program

**1.** Copy the code from the last step into a new Python file.

**2.** Remove all of the code **after** you have initialised the variables `left_sensor` and `right_sensor`.

**3.** After those variables have been defined, initialise the variables for controlling the speed of the motors and the timer:

~~~ python
speed = 0.75

duration = 10
end_time = time() + duration

running = True
~~~

The value for each motor will be modified by the `speed` multiplier to slow down the robot a little. The value for `speed` usually needs to be at least 0.6 otherwise the motors do not have enough momentum to turn on a solid surface, and the maximum value is 1.

The other variables are used to create a timer so that the robot doesn't run forever, just like the UDS program last week. Remember that `duration` is the number of seconds your program will run for, and you can modify this yourself.

### Planning a better program

To have more control over the robot's movement and speed, your program needs to choose how to instruct the motors based on the values from the line sensors.

Remember that when a line sensor is above a line, it outputs a `1`. When it’s off a line, it outputs a `0`. You can’t simply pass these values straight to the motors because the motors accept a range of values from `-1` to `1`; positive values tell the motor to run forwards and negative values run the motor in reverse.

Taking this behaviour into account, I am going to define three rules to determine what outputs are sent to the motors.

### The three rules to rule them all

**Rule 1:**

If both line sensors output `0`, then both motors should receive a positive value to drive forwards.

**Rule 2:**

If the left sensor outputs `1`, the robot has drifted right and needs to turn left. In this case, the left motor should run backwards (a negative signal is needed), while the right motor should run forwards.

**Rule 3:**

If the right sensor outputs `1`, the robot has drifted left and needs to turn right. Therefore, the right motor should run backwards (a negative signal is needed), while the left motor should run forwards.

![A table showing the robot directions based on the left line sensor and right line sensor readings.](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Illustration/37-3_9-table-sensor-values.png)

*Why do you think there is not a rule for both the sensors outputting a `1` simultaneously?*

### Programming the rules

To start applying these rules, the code needs to repeatedly read the outputs of the line sensors in a loop.

**4.** Add a `while` loop to the program after where you initialised the speed and timer variables.

~~~ python
while running:
    left_detect  = left_sensor.value
    right_detect = right_sensor.value

	print (left_detect, right_detect)
~~~

**5.** If you run the program now, you should see the binary output from the sensors change when you move the sensors over and off the line, in accoradance to the rules stated above. 

**6.** Inside the `while` loop, use conditional statements to specify the direction of each motor depending on the line sensor readings:

~~~ python
while running:
    left_detect  = left_sensor.value
    right_detect = right_sensor.value

    # Rule 1
    if left_detect == 0 and right_detect == 0:
        left_mot = 1
        right_mot = 1
    # Rule 2
    elif left_detect == 1:
        left_mot = -1
        right_mot = 1
    # Rule 3
    elif right_detect == 1:
        left_mot = 1
        right_mot = -1

	print (left_mot, right_mot)    
~~~

**7.** Run your code and test that the program outputs the correct motor values when you move the robot over and off the line.

**8.** Inside the loop, remove the `print` statement and replace it with:

~~~ python
    robin.left_motor.value = left_mot * speed
    robin.right_motor.value = right_mot * speed
~~~

The value for each motor will be modified by the `speed` multiplier to slow down the robot a little.

Make sure you remove any `print` statements within the loop otherwise this will affect the response time of the program and the robot may "overshoot" the line.

**9.** To stop the `while` loop from running forever, and to close all the component's connections cleanly, add this code inside the loop at the end:

~~~ python
    if time() >= end_time:
        running = False
        robin.stop()
        robin.close()
        left_sensor.close()
        right_sensor.close()
~~~

### Test your program

**10.** Now run your code and test your robot over a track.

Try different values for `speed` (between 0 and 1) and check how your robot runs.

**How does this affect your robot's ability to follow the line?**

Share your findings in the comments section.
