[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Testing the motors

You need to work out which is your left motor and which is right motor. You also need to know which way they are driving forwards and backwards.

You should already be familiar with turning on a Raspberry Pi and accessing the environment. If not, follow [this guide](https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started) to set up your Pi.

### Labelling the motors

Choose one of the motors. Use a marker pen to label it ‘right’ and draw an arrow on it to indicate which way is forward. Label the other motor ‘left’ and draw an arrow on it pointing in the same direction as your first one.

![Image of two motors: one with L and an arrow pointing up, the other with R and pointing up.](images/)

### Going forwards

**1.** On your Raspberry Pi, open a Python shell by clicking **Menu > Programming > Python 3 (IDLE)**. Then click **File > New File** to open an empty script.

**2.** In the new file, type the following to import the `Robot` class and create a `Robot` object. You can name it anything you like. In this course, I've chosen to call my robot `robin`.
<!-- can you name it robot or Robot?? -->

~~~ python
from gpiozero import Robot
robin = Robot(left=(7,8), right=(9,10))
~~~

**3.** Save your file and call it `robin.py` or something similar. You can then run it by pressing **F5** on your keyboard or clicking **Run > Run Module**.

**4.** Now switch over to the shell and type the following so that you can observe which way the motors turn.

~~~ python
robin.forward()
~~~

You can stop them by typing `robot.stop()` in the shell.

<!-- Return, Enter, new line - is it necessary to specify? -->

![Animated GIF showing the commands robin.forward() and robin-stop() being entered into the Python shell](images/)

### Left and right

**5.** Now, type the following command, and note which motor changes direction on the second command.

~~~ python
robin.forward(0.4)
robin.right(0.4)
~~~

The 0.4 makes the motors go a little slower, so it is easy to see which way they turn.

The motor that changed direction is the right-hand motor. If that was the one you labeled ‘right’, then there’s nothing to change yet. If it was the one you labeled ‘left’, you need to alter your Robot object in your file to switch around the left and right pin numbers:

~~~ python
# for example, change
robin = Robot(left=(7,8), right=(9,10))
# to
robin = Robot(left=(9,10), right=(7,8))
~~~

### Forward and backward

**6.** Now that you have the ‘left’ and ‘right’ motors sorted, you need to make sure you have forward and backward set up correctly.

Again drive both motors forward.

~~~ python
robin.forward(0.4)
~~~

Check that both motors are turning in the direction shown in the diagram below.

![Image showing the direction both the motors should be spinning when the command robin.forward(0.4) is entered](images/)

If the right-hand motor is turning in the wrong direction, alter your robot object by switching the order of the GPIO pin numbers. For instance:

~~~ python
# for example, change
robin = Robot(left=(9,10), right=(7,8))
# to
robin = Robot(left=(9,10), right=(8,7))
~~~

If the left-hand motor is turning the wrong way, then do the same thing and swap the order of the left pin numbers.

**7.** Test that the motors both turn backwards.

~~~ python
robin.backward(0.4)
~~~

If either of the motors does not turn backwards, try swapping the order of the GPIO pin numbers as in the example above. Make sure you test that the other commands still work correctly if you do swap the numbers!

### Setting the speed

You may have noticed that a value can be provided to the forward, backward, left, and right commands inside the brackets. Using a value that is less than 1 will make the motors turn at a slower speed than its default speed.

### Potential problems

If you are having problems with getting the motors to turn in the right direction, try following the instructions in this step again and save the code in a new Python file.

If the motors aren't moving at all, try one of the following things:

+ check that the wires from the motor board are connected to the four GPIO pins and GND as set out in the previous step
+ check the wires between the motors and the motor board are secure and connected properly
+ if the battery pack has a switch to turn it on and off, make sure it is switched on
+ most motor boards have a red LED to show it is powered on. If it is not lit up, you may need new batteries or your battery pack may need to be filled completely for it to work (e.g. if it has space for 8 batteries, then insert 8 batteries)

### Discussion

+ How many pin numbers did you have to change in your code?
+ What do you think is the advantage of swapping the pin numbers in the code rather than the wires of the motor?

Share your comments below.
