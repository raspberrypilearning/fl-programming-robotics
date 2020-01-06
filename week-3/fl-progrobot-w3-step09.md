[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Designing a more complex algorithm

The previous line following algorithm is okay, but as it runs the robot at full speed it's easy for the robot to "overshoot" the line. You can improve it by re-writing the program to read the values of the line sensors and use these to instruct which way each of the robot's left and right motors should turn.

### Planning a better algorithm

As previously discussed, when a line sensor is over the line, it outputs a `1` from the digital pin. When the sensor is off the line, it outputs a `0`.

![A still image from the animation in step 3.4 - 3_4_Two_Sensors_Anim.gif - with the left sensor (sensor 1) over the black line and the output as 1 and the right sensor (sensor 2) over the white surface with the output as 0](images/3_9-one-sensor-over-line)

The motors work on a range from `-1` to `1`; positive values tell the motor to run forwards and negative values run the motor in reverse.

**Rules of the algorithm**

+ If the robot is perfectly over the line, both line sensors are off the line (outputting `0`). The robot should continue going forward, so both motors should receive the same positive value.

+ If the robot has drifted to one side, the sensor on the opposite side will move over the line and so will output `1`. This results in two rules:
    + If the robot has drifted left, the right sensor will read `1`. To turn right, the right motor should run backwards (a negative signal is needed), while the left motor continues to run forwards.
    + If the robot drifted right, the opposite would be true.

*Why do you think there is not a rule for both the sensors outputting a `1` simultaneously?*

#### Getting the output from the sensors

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

Don’t forget to adjust the pin numbers if you’ve used different GPIO pins. You may also have renamed the variable `robin` to something else.

**2.** Run the code, then move the robot back and forth over the line to see what happens.

Hopefully, you should see the binary output from the sensors, similar to the video below:

![Video-gif of the robot sensors being moved slowly over and off the line with a shot of the output values on the screen changing whenever the robot is moved](images/3_9-binary-output-line-sensors)

#### Using the sensor readings to control the motors

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

<!-- Split the step here into another step? -->

#### Feeding the values to the motors

GPIO Zero provides a method for connecting devices together; feeding the values of one device into another. 

For example, the current `value` of a button can be used to set the `source` of values for an LED so that when the button is pressed, the LED turns on:

![Diagram showing a the values of a button feeding the source of an LED](https://gpiozero.readthedocs.io/en/stable/_images/led_button.svg)

To do this, you are going to turn your `while` loop into a **generator**. A generator is a special type of function that produces a series of values over time.



an **iterator**, such as a 



The `source` of an output device must be set by an **iterator**, such as a list of items. In your program, you are going to specify the `source` of the motors by turning the `while` loop into a **generator**, which is a special type of function that returns an iterator.

These values can also be processed before they are passed to the source of an output device.



To do this with the motors, you are going to produce a series of values from the line sensors 


In your program, the iterator will be a series of values produced by the line sensors. 


To set the `source` of the motors, you are going to produce a series of values


You are going to produce a series of values from the line sensors


To do this using the line sensor values, you are going to turn the `while` loop into a **generator**, which is a special type of function that returns an iterator.

These values can also be processed before they are passed to the source of an output device.

![Diagram showing the values of an input device being processed with a custom generator and then passed to the source of an output device](https://gpiozero.readthedocs.io/en/stable/_images/value_processing.svg)

**5.** Turn your loop into a generator using the code below:

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




A generator is a special kind of function, except that it uses the `yield` statement instead of `return` to send values back to the function call. 





The `source` of values for the output device are produced by a **generator**, which is a special type of function. 




This can be done by setting the `source` of values for an output device 

The `source` of values for the output device


To do this, you need to set the `source` of the output device using an **iterator**. 


To do this with your line following algorithm, you’re going to turn your `while True` loop into a **generator**. 



which can be produced by a **generator**. 

using a **generator** and an **iterator**.



an **iterator** instead of the value of a variable.



The values of the input device can also be processed before they are passed to the source of the output device.






To do this with your line following algorithm, you’re going to turn your `while True` loop into a **generator**. 

![Diagram showing the values of an input device being processed with a custom generator and then passed to the source of an output device](https://gpiozero.readthedocs.io/en/stable/_images/value_processing.svg)

A generator is a special kind of function, except that it uses the `yield` statement instead of `return` to send values back to the function call. 

Generators are useful when you need to produce a series of values over time, rather than a single value, but don’t want to store the entire sequence in memory.

The yield statement suspends the function's execution by saving the current state of the function instead of stopping it.

Let's see how you can use a generator practically for your line sensing robot.

**6.** Turn your loop into a generator using the code below:

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

In this code, the `yield` statement produces values for the robot's right and left motors whenever the generator `motor_speed()` is called. 

The last line of code sets the `source` of the robot’s motor values to the result of the generator. 

Just like the `when_line` and `when_no_line` events from before, `source` will retain the last value supplied and continue to run even after you close the program.

**7.** To make sure that the robot doesn’t keep running forever, and to close all the components connections cleanly, add in these lines to the end of your program:

~~~ python
sleep(60)

robin.stop()
robin.source = None
robin.close()
left_sensor.close()
right_sensor.close()
~~~

Setting the robot's `source` to `None` before closing the robot connection safely terminates the event.

Remember, you can change the number of seconds of `sleep` to a different value if you want to test the robot for shorter or longer periods of time.

**8.** Now run your code and test your robot over a track.

#### Reducing the speed

Sometimes the robot runs a little too fast, so you can tweak your code a bit as shown in the following completed script. 

**9.** Add in a speed multiplier to slow the robot down a little.

~~~ python
from gpiozero import Robot, LineSensor
from time import sleep

robin = Robot(left=(8, 7), right=(9, 10))
left_sensor = LineSensor(19)
right_sensor= LineSensor(26)

speed = 0.65

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
        yield (right_motor * speed, left_motor * speed)

robin.source = motor_speed()

sleep(60)

robin.stop()
robin.source = None
robin.close()
left_sensor.close()
right_sensor.close()
~~~

<!-- Add content to below points if this step is split into two -->

### Taking it further

+ Using a line following PID array sensor

+ Reading the proportional value of the robot’s position compared to the line

+ Calculating the derivative value (i.e. rate of change) using the setpoint value and the current value

+ Adjusting the direction based on the derivative

+ Testing and refining the equation and algorithm
