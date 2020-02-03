[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Making the robot move

Now you are going to test whether your buggy can move forward, backward, left and right using the Python program you created for testing the motors. First though, find a suitable surface for the buggy to move on and then power up the Pi and motor controller.

### Finding a suitable surface

Typically, the motors and wheels used for a robot buggy aren't very good when moving on certain surfaces, such as carpet. If possible, I recommend testing the buggy on a large wooden surface or tilled floor.

### Powering the Raspberry Pi and motor controller

Power up your Raspberry Pi and the motor controller board. Remember, you will need a mobile power supply for the Pi otherwise the buggy will not be able to travel far from the mains plug.

If either of the wheels starts spinning continuously, chances are one of the connections between the motor controller and the Raspberry Pi has come loose or is wired up wrong. Turn off the battery pack for the motor controller or remove the power from the Raspberry Pi to stop the motors. Then, check the wiring that you connected in the steps for connecting the motors and the Raspberry Pi to the motor controller.

### Testing the movement

To check whether your buggy can move in all directions, it is best to use one of the programs you created for testing the direction of the motors - just make sure it was a working program with the correct GPIO pins for the `Robot`!

You need to check that the buggy can move in every direction. Therefore, a program that contains the commands `.foward()`, `.backward()`, `.left()` and `.right()` is ideal. Remember to end the program with `.stop()` to stop the motors from turning.

If you don't have a program that is suitable, you can copy the code below into a new Python file. However, you may need to adjust the GPIO pins for the `left` and `right` motors like you did earlier. For example, in my robot setup I had to swap the `left` motor pins from `7,8` to `8,7`.

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

![Video of the buggy moving forward, right, backward and left](images/1_10-buggy-moving-all-four-directions)

**Does the robot buggy move forward, backward, left and right correctly in the order you specified in the code?**

If not, check that the GPIO pins of the `left` and `right` arguments of the `Robot` are set correctly for your motors. Follow the previous instructions when you tested the direction of both motors if you are still having issues.

**Does the speed need adjusting?**

In the code above, I specified a speed that is lower than the default speed of 1 using the commands `.right(0.8)`, `.backward(0.9)` and `.left(0.7)`. If your buggy doesn't turn or move backward as intended, try changing the values inside the brackets and then run the program again to see any changes made.

### Understanding how the .forward(), .left(), .right() and .backward() commands work

Using `Robot` from the GPIO Zero library allows you to set the direction of the motors without needing to worry too much about the signals being sent to the motors.

As useful as this is, it's also important to understand how these signals are interpreted by the motor controller board to produce the output you want.

The motors work on a range of `-1` to `1`; positive values tell the motor to run forwards and negative values run the motor in reverse.

When using the `.forward()` command, a positive value is sent to the left and right motors, whilst the `.backward()` command sends a negative value to both motors.

The `.left()` and `.right()` commands work a bit differently. To turn left, the left motor needs to run backwards (a negative signal is needed), while the right motor should run forwards. The opposite is true to turn right; the right motor receives a negative value and the left motor a positive value.

### Connecting to a Raspberry Pi remotely

Being able to connect to your Raspberry Pi remotely is really useful when designing, running and testing code on the robot buggy. It means you don't have to or remove your Pi from the buggy every time you want to run or edit a program.

To use your Raspberry Pi without physically connecting it to a monitor, mouse or keyboard, you can remotely access the Pi via SSH (Secure Shell) or VNC (Virtual Network Computing).

VNC is a graphical desktop sharing system that allows you to remotely control the desktop interface of one computer (running VNC Server) from another computer or mobile device (running VNC Viewer). For more information, read our guide on [Connecting to your Raspberry Pi with VNC Viewer](https://www.raspberrypi.org/documentation/remote-access/vnc/README.md).

You can also access the command line of a Raspberry Pi remotely from another computer or device on the same network using SSH. However, you will only have access to the command line, not the full desktop environment. Our guide on [Connecting to Raspberry Pi via SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) contains more details on how to do this.

Share how you got on and any issues you are having in the comments below. Post a link to a video of your robot once you have got it moving!
