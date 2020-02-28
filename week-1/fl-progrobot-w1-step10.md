[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Making the robot move

Now you are going to test whether your buggy can move forwards, backwards, left, and right, using the Python program you created for testing the motors.

### Finding a suitable surface

Typically, the motors and wheels used for a robot buggy aren't very good at moving on certain surfaces, such as carpet. If possible, I recommend testing the buggy on a large wooden surface or a tiled floor.

### Powering the Raspberry Pi and motor controller

Power up your Raspberry Pi and the motor controller board. Remember, you will need a mobile power supply for the Pi, or your robot will not be able to travel far from the mains plug.

If either of the wheels starts spinning continuously, chances are one of the connections between the motor controller and the Raspberry Pi has come loose, or is wired up wrongly. Turn off the battery pack for the motor controller or remove the power from the Pi to stop the motors. Then check the wiring that you connected in the steps for connecting the motors and the Raspberry Pi to the motor controller.

### Testing the movement

To check whether your buggy can move in all directions, it is best to use one of the programs you created for testing the direction of the motors; just make sure it was a working program with the correct GPIO pins for the `Robot`!

You need to check that the buggy can move in every direction. Therefore, a program that contains the commands `.forward()`, `.backward()`, `.left()`, and `.right()` is ideal. Remember to end the program with `.stop()` to stop the motors from turning.

If you don't have a program that is suitable, you can copy the code below into a new Python file (adjusting the GPIO pin numbers as needed).

~~~ python
from gpiozero import Robot
from time import sleep

robin = Robot(left=(8,7), right=(9,10))

robin.forward()
sleep(1)

robin.right(0.8)
sleep(1)

robin.backward(0.9)
sleep(1)

robin.left(0.7)
sleep(1)

robin.stop()
~~~

![Video of the buggy moving forward, right, backward and left](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/1_10-buggy-moving-all-four-directions.gif)

Does the robot buggy move forwards, backwards, left, and right correctly, in the order you specified in the code?

If not, check that the GPIO pins of the `left` and `right` arguments of the `Robot` are set correctly for your motors. For example, in my robot set-up I had to swap the `left` motor pins from `7,8` to `8,7`. If you are still having issues, follow the instructions that you used previously when you tested the direction of both motors.

If your buggy moves for some but not all of the commands, try adjusting the number given in the brackets, which controls the speed of the motors.

### Understanding how the .forward(), .left(), .right(), and .backward() commands work

Using `Robot` from the GPIO Zero library allows you to set the direction of the motors without worrying too much about the signals being sent to the motors.

As useful as this is, it's also important to understand how these signals are interpreted by the motor controller board to produce the output you want.

The motors work on a range of `-1` to `1`; positive values tell the motor to run forwards, and negative values tell the motor to run in reverse. The size of the value adjusts the speed of the motors.

When using the `.forward()` command, a positive value is sent to both motors, while the `.backward()` command sends a negative value to both.

The `.left()` and `.right()` commands work a bit differently. To turn left, the left motor needs to run backwards (a negative signal is needed), while the right motor should run forwards. The opposite is true to turn right; the right motor needs to receive a negative value and the left motor a positive value.

### Connecting to a Raspberry Pi remotely

Being able to connect to your Raspberry Pi remotely is useful when designing, running, and testing code on the robot buggy. It means you don't have to remove the Raspberry Pi from the buggy every time you want to run or edit a program.

To use your Raspberry Pi without physically connecting it to a monitor, mouse, or keyboard, you can remotely access the Pi via VNC (Virtual Network Computing) or SSH (Secure Shell).

VNC is a system that allows you to control remotely the graphical desktop interface of one computer (running VNC Server) from another computer or mobile device (running VNC Viewer). For more information, read our guide on [Connecting to your Raspberry Pi with VNC Viewer](https://www.raspberrypi.org/documentation/remote-access/vnc/README.md).

You can also access the command line (but not the graphical interface) of a Raspberry Pi remotely from another device on the same network, using SSH. Our guide on [Connecting to Raspberry Pi via SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) contains the details of how to do this.

### Discussion

Share how you got on and any issues you are having in the comments below. Post a link to a video of your robot once you have got it moving! You may need to use a video-hosting platform such as [YouTube](http://www.youtube.com).
