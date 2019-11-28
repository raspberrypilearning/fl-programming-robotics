[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Making the robot move

Now that you've constructed your buggy you are going to test whether it can move forward, backward, left and right, by using the Python program you created earlier.

### Finding a suitable surface

Typically, the motors and wheels used for a robot buggy aren't very good when moving on certain surfaces, such as carpet. If possible, I recommend testing the buggy on a large wooden surface, or a tiled floor.

### Powering the Raspberry Pi and motor controller

Power up your Raspberry Pi and the motor controller board. Remember, you will need a mobile power supply for the Pi otherwise the buggy will not be able to travel far from the mains plug.

If either of the wheels starts spinning continuously, it's likely that one of the connections between the motor controller and the Raspberry Pi has come loose or is wired up wrong. Turn off the battery pack for the motor controller or remove the power from the Raspberry Pi, and check the wiring.

### Testing the movement

To check whether your buggy can move in all directions, it is best to adapt one of the programs you created in step 1.7. Make sure the program is one that was working when you tested the motor directions previously.

You need to check that the buggy can move in every direction. This means that a program that contains all of the commands `.foward()`, `.backward()`, `.left()` and `.right()` is ideal. Remember to end the program with `.stop()` to stop the motors from turning.

If you don't have a program that is suitable, you can copy the code below into a new file. However, the numbers of your GPIO pins set in the `left` and `right` arguments of the `Robot` in line 2 may not be the same as mine or in a different order.

~~~ python
from gpiozero import Robot
robin = Robot(left=(7,8), right=(9,10))

robin.forward()
sleep(1)
robin.right(0.4)
sleep(1)
robin.backward(0.6)
sleep(1)
robin.left(0.4)
sleep(1)
robin.stop()
~~~

**Does the robot buggy move forward, backward, left and right correctly in the order you specified in the code?**

If not, check that the GPIO pins of the `left` and `right` arguments of the `Robot` are set correctly for your motors. Follow the instructions again in step 1.7 if you are still having issues.

**Does the speed need adjusting?**

In the code above, I specified a speed that is lower than the default speed of 1 in the commands `.right()`, `.backward()` and `.left()`. If your buggy doesn't turn or move backward as intended, try changing the values and then run the program again to see any changes made.

### Connecting to a Raspberry Pi remotely

Being able to connect to your Raspberry Pi remotely is really useful when designing, running and testing code on the robot buggy. It means you don't have to remove your Pi from the buggy every time you want to run or edit a program.

To use your Raspberry Pi without physically connecting it to a monitor, mouse or keyboard, you can remotely access the Pi via SSH (Secure Shell) or VNC (Virtual Network Computing).

VNC is a graphical desktop sharing system that allows you to remotely control the desktop interface of one computer (running VNC Server) from another computer or mobile device (running VNC Viewer). For more information, read our guide on [Connecting to your Raspberry Pi with VNC Viewer](https://www.raspberrypi.org/documentation/remote-access/vnc/README.md).

You can also access the command line of a Raspberry Pi remotely from another computer or device on the same network using SSH. However, you will only have access to the command line, not the full desktop environment. Our guide on [Connecting to Raspberry Pi via SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) contains more details on how to do this.
