[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Designing a more complex algorithm

The previous line following algorithm is okay, but as it runs the robot at full speed it's easy for the robot to "overshoot" the line. You can improve it by re-writing it to read the values of the line sensors and use these to instruct the robot's left and right motors which way each one should turn.


### Planning a better algorithm

As previously discussed, when a line sensor is over the line, it outputs a `1` from the digital pin. When the sensor is off the line, it outputs a `0`.

![A still image from the animation in step 3.4 - 3_4_Two_Sensors_Anim.gif - with the left sensor (sensor 1) over the black line and the output as 1 and the right sensor (sensor 2) over the white surface with the output as 0](images/3_9-one-sensor-over-line)

The motors work on a range from `-1` to `1`, positive values tell the motor to run forwards and negative values run the motor in reverse.

#### Rules of the algorithm

+ If the robot is perfectly over the line, both line sensors are off the line (outputting `0`). The robot should continue going forward, so both motors should receive the same positive value.
+ If the robot has drifted to one side, the sensor on the opposite side will move over the line and so will output `1`. For example if the robot has drifted left, the right senor will read `1`. To turn right, the right motor should run backwards (a negative signal is needed), which the left motor continues to run forwards.
+ If the robot drifed right, the opposite would be true.

*Why do you think there is not a rule for both the sensors outputting a `1` simultaneously?*

#### Getting the output from the sensors

To apply these rules, the code needs to repeatedly read the outputs of the line sensors, in a loop:

~~~ python
from gpiozero import Robot, LineSensor
from time import sleep

robin = Robot(left=(8, 7), right=(9, 10))
left_sensor = LineSensor(19)
right_sensor= LineSensor(26)

for i in range(1000):
	left_detect  = int(left_sensor.value)
	right_detect = int(right_sensor.value)
	print(left_detect, right_detect)
~~~

Don’t forget to adjust the pin numbers if you’ve used different GPIO pins. You may also have renamed the variable `robin` to something else.

**2.** Run the code, then move the robot back and forth over the line to see what happens.

Hopefully, you should see the binary output from the sensors, similar to the video below:

![Video-gif of the robot sensors being moved slowly over and off the line with a shot of the output values on the screen changing whenever the robot is moved](images/3_9-binary-output-line-sensors)

#### Using the sensor readings to control the motors

Your next step is to send a signal to the

+ If both sensors output `0`, then both motors should receive `1`
+ If the right sensor outputs `1`, then the left motor should receive `-1` and the right motor `1`
+ If the left sensor outputs `1`, then the left motor should receive `1` and the right motor `-1`

The signals for the motors should be stored in two new variables - I've called them `left_motor` and `right_motor`.

**3.** Inside the `for` loop, use conditional statements to work out which way your robot needs to go:

~~~ python
for i in range(1000):
	left_detect  = int(left_sensor.value)
	right_detect = int(right_sensor.value)

  if left_detect == 1:
    left_motor = -1
    right_motor = 1
  elif right_detect == 1:
    left_motor = 1
    right_motor = -1
  elif left_detect == 0 and right_detect == 0:
    left_motor = 1
    right_motor = 1

  sleep 0.01
~~~

**4.** Run your code and test how it works when you move the robot over the line.

### Feeding the values to the motors

GPIO Zero provides a method for connecting devices together, allowing the `value` of an input device to set the state of an output device.

For example, the input values of a button could be fed into an LED so that when the button is pressed, the LED turns on:

![Diagram showing a the value of a button feeding the source of an LED](https://gpiozero.readthedocs.io/en/stable/_images/led_button.svg)

The values of the input device can also be processed before they are passed to the source of the output device.

In your code you can do this by adding:

~~~python
  motor_speed = (right_motor, left_motor)
  robin.source = motor_speed()
~~~

just before the sleep statement in the loop.

Just like when you set the motors earlier, `source` will retain the last value supplied and continue to run even after you close the program.

**7.** To make sure that the robot doesn’t keep running forever, and to close all the components connections cleanly, add in these lines after the loop:

~~~ python
robin.source = None
robin.close()
left_sensor.close()
right_sensor.close()
~~~

Setting the robot's `source` to `None` before closing the robot connection safely terminates the event.

Remember, you can change the repeats of the loop to a different value if you want to test the robot for shorter or longer periods of time.

**8.** Now run your code and test your robot over a track.

#### Reducing the speed

Sometimes the robot runs a little too fast, so you can tweak your code a bit as shown in the following completed script.

**9.** Add in a speed multiplier to slow the robot down a little. Try different values for `speed` (between 0 and 1) and check how your robot runs.

~~~ python
speed = 0.65
motor_speed = (right_motor*speed, left_motor*speed)
~~~



<!-- DELETE -->
You can also process the values from the line sensors before they are passed to the `source` of the motors.

![Diagram showing the values of an input device being processed with a custom generator and then passed to the source of an output device](https://gpiozero.readthedocs.io/en/stable/_images/value_processing.svg)
