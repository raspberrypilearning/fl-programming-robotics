[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Testing the motors

In this step you will choose one of the motors to be the left motor and the other one to be the right motor. You will then use the Raspberry Pi to program the motors so that the robot buggy is able to go forward, backward, left and right.

### Labelling the motors

The easiest way to keep track of which motor is left and which is right is to label the motors.

+ Start by lining up the motors side-by-side
+ Use a marker pen to label the motor on the left-hand side ‘left’ and draw an arrow on it to indicate which way is forward, just like in the animation below
+ Label the other motor ‘right’ and draw an arrow on it pointing in the same direction as your first motor

![Picture of two motors: one with L and an arrow pointing up, the other with R and an arrow pointing up](images/1_7-labelled-motors)

### Choosing a programming environment

I recommend using an Integrated Development Environment (IDE) during this course to create, run and test your Python programs.

The IDE I will be using is **Mu**, which is preinstalled on most Raspberry Pis. Mu is also available at the website [codewith.mu](https://codewith.mu/) along with [Instructions on how to install Mu on a Raspberry Pi](https://codewith.mu/en/howto/1.0/install_raspberry_pi).

If you experience problems or would just like to know more about Mu, have a look at Raspberry Pi’s [Getting started with Mu](https://projects.raspberrypi.org/en/projects/getting-started-with-mu) guide.

**Note:** if you choose another IDE, some of the screenshots and instructions in this course might differ to your development environment.

### Programming the motors

#### Setting up the motors in Python

You are going to start by creating a Python program that allows the motors to be controlled through the GPIO pins on the Raspberry Pi.

**1.** On your Raspberry Pi, open Mu or the IDE of your choice and create a new file.

**2.** In the new file, type in the following code:

~~~ python
from gpiozero import Robot
robin = Robot(left=(7,8), right=(9,10))
~~~

The first line of code imports `Robot` from the GPIO Zero library, which you will use to control the direction and speed of the motors.

The second line of code sets the GPIO pins of the motors that the `Robot` is interacting with. You can name the variable anything you like - in this course, I've chosen to call my robot `robin`.

When defining the `Robot` in the code you need to give it two arguments: `left` and `right`. The `left` argument should specify the two GPIO pins on the Raspberry Pi that are connected to the pins labelled **IN1** and **IN2** on the motor controller. In the last step, I chose GPIO pins 7 and 8 but yours might be different.

Similarly, the `right` argument needs to specify the GPIO pins that are connected to the pins labelled **IN3** and **IN4** on the motor controller - for me that is GPIO pins 9 and 10.

**3.** Save your file and call it `robin.py` or something similar.

#### Forward and backward

You are now going to test which direction is forward and backward on each motor. This will depend on how the motors are wired and the code in your program.

**4.** At the end of your program, type in this code to drive both motors forward at the default speed, wait 1 second and then stop the motors:

~~~ python
robin.forward()
sleep(1)
robin.stop()
~~~

**Note:** `robin` is the name I gave my `Robot` in the first piece of code - if you chose a different name then make sure you change `robin` to the name you specified.

The `sleep` command waits for a given number of seconds before running the next command - in this example, the program waits 1 second before stopping both motors with the command `robin.stop()`.

Run the program and check that both motors are turning in the direction shown in the diagram below in relation to the arrows you drew on the motors.

![Picture with arrows showing the direction both the motors should be spinning when the forward() command is entered](images/1_7-motors-spinning-forward)

If the right-hand motor is turning in the wrong direction, alter your `Robot` code and swap the order of the right pin numbers.

~~~ python
# for example, change the right pins from
robin = Robot(left=(9,10), right=(7,8))
# to
robin = Robot(left=(9,10), right=(8,7))
~~~

If the left-hand motor is turning the wrong way, then do the same thing and swap the order of the left pin numbers.

**Note:** You may have chosen different GPIO pins than me to connect the Raspberry Pi to the motor controller.

Stop the program and run it again to check how any changes you made affected the motors.

**5.** Test that the motors both turn backwards by adding `robin.backward()` and another `sleep` command before `robin.stop()`, and running the program.

~~~ python
robin.forward()
sleep(1)
robin.backward()
sleep(1)
robin.stop()
~~~

You should see both the motors turn forwards, wait 1 second and then turn the opposite way for 1 second before stopping.

If the both motors do not turn as expected, repeat steps 4 and 5 until both motors turn forward and backward correctly.

#### Left and right

Finally, you are going to test whether the motors are turning the correct way when using the `.left()` and `.right()` commands.

**6.** Type the following lines of code at the end of the Python file you created. Run the program and note which motor changes direction on the command `robin.right(0.6)`.

~~~ python
robin.forward(0.6)
sleep(1)
robin.right(0.6)
sleep(1)
robin.stop()
~~~

**Note:** The 0.6 inside the `.forward()` and `.right()` commands makes the motors go a little slower, so it is easier to see which way they turn. The default speed is 1.

The motor that changed direction is the right-hand motor. If that was the one you labelled ‘right’, then there’s nothing to change. If it was the one you labelled ‘left’, you need to alter your `Robot` code to swap the left pin numbers with the right pins:

~~~ python
# for example, change the GPIO pins from
robin = Robot(left=(7,8), right=(9,10))
# to
robin = Robot(left=(9,10), right=(7,8))
~~~

Remember, you may have chosen different GPIO pins than me to connect the Raspberry Pi to the motor controller. Your pin numbers may also have been altered when setting up the forward and backward directions.

Stop the program and run it again to check how any changes you made affected the motors. Repeat step 6 if you made any changes.

**7.** Check that the left motor is turning correctly by adding the `.left()` command to the program.

~~~python
robin.forward(0.8)
sleep(1)
robin.left(0.7)
sleep(1)
robin.stop()
~~~

The motor that changed direction at the end of the program should be the motor you labelled ‘left’.

#### Potential problems

If you are having problems with getting the motors to turn in the right direction, try out the instructions for programming the motors again and save the code in a new Python file.

**Top tip:** if there is a problem with your program or the wiring, the motors can spin continuously. If this happens, try entering the command `robin.stop()` (or the name you gave the robot object followed by `.stop()`) into the Python shell (known as the REPL in Mu). Otherwise, turn off the battery pack or Raspberry Pi and check the wiring is correct.

If the motors aren't moving at all, try the following :

+ Check that the wires from the motor controller are connected to the four GPIO pins and GND as set out in the previous step
+ Check the wires between the motors and the motor controller are secure and connected properly
+ If the battery pack has a switch to turn it on and off, make sure it is switched on
+ Most motor controllers have a red LED to show it is powered on. If it is not lit up, you may need new batteries or your battery pack may need to be filled completely for it to work (e.g. if it has space for 8 batteries, then insert 8 batteries)

### Challenge: experimenting with direction and speed

+ Create a Python file that includes each of the commands: `forward`, `backward`, `left` and `right`.

+ Experiment with giving these commands different values inside the brackets e.g. `robin.left(0.65)`

Do you need any help? Share any issues you have below with your fellow learners.