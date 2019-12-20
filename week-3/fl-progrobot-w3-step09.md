[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Designing a more complex algorithm



You are now going to code, test, and refine an algorithm so that your buggy is able to follow the line of your track. 


### Planning a better algorithm

+ Reading the data from the line sensors

+ Using 1s and 0s from the line sensor values to modify the robot movement


<!-- Taken from AliExpress -->
The Line Tracking Sensor for Arduino can detect the white lines in black background and black lines in white background.
If Line Tracking Sensor detect black color, the signal line (DO) of the sensor is HIGH,  at the same time the LED (blue) on the sensor lights up. If Line Tracking Sensor detect white color, the signal line (DO) goes LOW.


For this algorithm, the buggy should move forwards if no line has been detected (as it should be directly over the line). If the left sensor detects the line, your buggy should move to the left until it is not over the line. Whilst the right sensor detects the line, your buggy should move to the right.


### Taking it further

+ Using a line following PID array sensor

+ Reading the proportional value of the robot’s position compared to the line

+ Calculating the derivative value (i.e. rate of change) using the setpoint value and the current value

+ Adjusting the direction based on the derivative

+ Testing and refining the equation and algorithm


