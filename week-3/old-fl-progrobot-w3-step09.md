[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Designing a more complex algorithm

The previous line following algorithm is okay, but it can easily be improved upon. To do this, you are going to read the values of the line sensors and use these to instruct the robot's left and right motors which way each one should turn.

### Planning a better algorithm

As previously discussed, when a line sensor is over the line, it outputs a `1` from the digital pin. When the sensor is off the line, it outputs a `0`.

![A still image from the animation in step 3.4 - 3_4_Two_Sensors_Anim.gif - with the left sensor (sensor 1) over the black line and the output as 1 and the right sensor (sensor 2) over the white surface with the output as 0](images/3_9-one-sensor-over-line)

The motors work slightly differently though; whenever the robot receives a `1` signal to a motor, that motor drives `forward`. Whenever the robot receives a `-1`, it drives that motor `backward`. 

#### Rules of the algorithm

Let’s have a look at an algorithm that takes into account the position of the robot, the states of the lines sensors, and the actions required of the motors.

1. The robot is perfectly on the line and should drive forwards:
    + Both line sensors are off the line and outputting a `0`
    + Both motors should receive `1` to drive forwards
2. The robot has drifted left and needs to **turn right**:
    + The right sensor is over the line and outputting a `1`
    + The left sensor is off the line and outputting a `0`
    + The left motor should run backwards and so receive a `-1`
    + The right motor should run forwards and so receive a `1`
3. The robot has drifted right and needs to **turn left**:
    + The right sensor is off the line and outputting a `0`
    + The left sensor is over the line and outputting a `1`
    + The left motor should run forwards and so receive a `1`
    + The right motor should run backwards and so receive a `-1`

*Why do you think there is not a rule for both the sensors outputting a `1` simultaneously?*

#### Getting the output from the sensors

How can you apply these rules to a piece of code? First of all, you’ll create an infinite loop to view the sensor values.

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

So now that you have the output of the sensors, you need to alter these values before you send them to the motors. As per the algorithm above:

+ If both sensors output `0`, then both motors should receive `1`
+ If the right sensor outputs `1`, then the left motor should receive `-1` and the right motor `1`
+ If the left sensor outputs `1`, then the left motor should receive `1` and the right motor `-1`

To implement these conditions in the program, you will also need two new variables called `left_motor` and `right_motor`. The values of these variables will be used to instruct the motors of the robot which way to turn.

**3.** Inside the `while` loop, use a condition to check if both sensors are not over the line.

~~~ python
while True:
	left_detect  = int(left_sensor.value)
	right_detect = int(right_sensor.value)

	if left_detect == 0 and right_detect == 0:
		left_motor = 1
		right_motor = 1
~~~

*What do you think the other two conditions will look like?*

Use the rules of the algorithm to specify the direction of each motor when the robot has drifted to the left or right of the line.

**4.** You need two more if statements to handle the sensors being triggered by a line.

~~~ python
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

	print (right_motor, left_motor)
~~~

For now, you can simply print out their values within the loop. Notice that the values are being printed out in the order `right_motor, left_motor`. This is important for the next stage of the code.

**5.** Run your code and test how it works when you move the robot over the line.

<!-- Split the step here into another step? -->

#### The final algorithm

Now that you are specifying values that the motors can use, it is time to feed these values to the motors.

GPIO Zero provides a method for connecting devices together, allowing the `value` of an input device to set the state of an output device.

For example, the input values of a button could be fed into an LED so that when the button is pressed, the LED turns on:

![Diagram showing a the value of a button feeding the source of an LED](https://gpiozero.readthedocs.io/en/stable/_images/led_button.svg)

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
