[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Designing a more complex algorithm

The previous line following algorithm is okay, but the robot can move a bit jaggedly especially when following a curved track / around corners.


The previous line following algorithm is okay, but as it runs the robot at full speed it's easy for the robot to "overshoot" the line. 

To have more control over the robot's speed and run time, you can modify the program so that it reads the values of the line sensors and uses these to instruct which way each of the robot's left and right motors should turn.

### Planning a better algorithm

As previously discussed, when a line sensor is over the line, it outputs a `1` from the digital pin. When the sensor is off the line, it outputs a `0`.

![A still image from the animation in step 3.4 - 3_4_Two_Sensors_Anim.gif - with the left sensor (sensor 1) over the black line and the output as 1 and the right sensor (sensor 2) over the white surface with the output as 0](images/3_9-one-sensor-over-line)

The motors work on a range from `-1` to `1`; positive values tell the motor to run forwards and negative values run the motor in reverse.

**Rules of the algorithm**

+ If the robot is perfectly over the line, both line sensors are off the line (outputting `0`). The robot should continue going forward, so both motors should receive the same positive value.

+ If the robot has drifted to one side, the sensor on the opposite side will move over the line and so will output `1`. This means that:
    + if the robot has drifted left, the right sensor will read `1`. To turn right, the right motor should run backwards (a negative signal is needed), while the left motor continues to run forwards.
    + if the robot drifted right, the opposite would be true.

*Why do you think there is not a rule for both the sensors outputting a `1` simultaneously?*

#### Reading the values of the sensors

To apply these rules, the code needs to repeatedly read the outputs of the line sensors, in a loop:

**1.** In a new Python 3 file, add in the following lines of code:

~~~ python 
from gpiozero import Robot, LineSensor
from time import sleep

robin = Robot(left=(8, 7), right=(9, 10))
left_sensor = LineSensor(19)
right_sensor= LineSensor(26)

while True:
	left_detect  = int(left_sensor.value)
	right_detect = int(right_sensor.value)
	print(left_detect, right_detect)
~~~

Don’t forget to adjust the pin numbers if you’ve used different GPIO pins. 

**2.** Run the code, then move the robot back and forth over the line to see what happens.

Hopefully, you should see the binary output from the sensors, similar to the video below:

![Video-gif of the robot sensors being moved slowly over and off the line with a shot of the output values on the screen changing whenever the robot is moved](images/3_9-binary-output-line-sensors)

#### Using the sensor readings to set the motor values

Your next step is to send a signal to the motors:

+ If both sensors output `0`, then both motors should receive `1`
+ If the right sensor outputs `1`, then the left motor should receive `-1` and the right motor `1`
+ If the left sensor outputs `1`, then the left motor should receive `1` and the right motor `-1`

The signals for the motors should be stored in two new variables - I've called them `left_motor` and `right_motor`.

**3.** Inside the `while` loop, use conditional statements to work out which way your robot needs to move:

~~~ python
while True:
	left_detect  = int(left_sensor.value)
	right_detect = int(right_sensor.value)

	if left_detect == 0 and right_detect == 0:
		left_motor = 1
		right_motor = 1
	elif right_detect == 1:
		left_motor = -1
		right_motor = 1
	elif left_detect == 1:
		left_motor = 1
		right_motor = -1

	print (right_motor, left_motor)    
~~~

Notice that the signals are being output in the order `right_motor, left_motor`. This is important for the next stage of the code.

**4.** Run your code and test how it works when you move the robot over the line.

#### Generating the source values of the motors

GPIO Zero allows you to set the `source` of an output device so that it can receive a series of values over time. 

|In your program, you are going to set the `source` of values for the motors depending on the current `value` of the line sensors. 

**5.** To do this, you will need to turn your `while` loop into a **generator**:

~~~ python
def motor_speed():
    while True:
        left_detect  = int(left_sensor.value)
        right_detect = int(right_sensor.value)
        
        if left_detect == 0 and right_detect == 0:
            left_motor = 1
            right_motor = 1
        
        if left_detect == 0 and right_detect == 1:
            left_motor = -1
            right_motor = 1
        
        if left_detect == 1 and right_detect == 0:
            left_motor = 1
            right_motor = -1
        
        # values need to be in the order right, left for the robin.source event
        yield (right_motor, left_motor)

robin.source = motor_speed()
~~~

You may be more used to seeing `return` to pass values back from functions. 

A **generator** is a special kind of function that uses `yield` to return data instead.

The data returned to the function call is an **iterator**, which is a series of values, rather than a single value. 

This iterator is then used to update the `source` of the motor's value over time.

#### Specifying a time limit

Just like when you set the motors earlier, `source` will retain the last value supplied and continue to run even after you close the program.

**7.** To make sure that the robot doesn’t keep running forever, add this code to the end of your program:

~~~ python
sleep(60)

robin.stop()
robin.source = None
robin.close()
left_sensor.close()
right_sensor.close()
~~~

Remember, you can change the number of seconds within `sleep` if you want to test the robot for shorter or longer periods of time.

**8.** Now run your code and test your robot over a track.

#### Reducing the speed

Sometimes the robot runs a little too fast, so you can tweak your code to slow the robot down.

**9.** Add in a speed multiplier to the program. Try different values for `speed` (between 0 and 1) and check how your robot runs.

~~~ python
speed = 0.65

yield (right_motor * speed, left_motor * speed)
~~~
