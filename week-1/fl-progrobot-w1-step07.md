[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Testing the motors

In this step you will label and test the motors, to help ensure that your robot will correctly go forwards, backwards, left, or right as commanded.

### Labelling the motors

The easiest way to keep track of which motor is left and which is right is to label them.

+ Line the motors up side by side
+ Use a marker pen to label the left-hand motor ‘left’ and draw an arrow on it to indicate which way is forward, as shown below
+ Label the other motor ‘right’ and draw an arrow on it pointing in the same direction as your first motor

![Picture of two motors: one with L and an arrow pointing up, the other with R and an arrow pointing up](images/1_7-labelled-motors)

### Programming the motors

#### Setting up the motors in Python

1. On your Raspberry Pi, open Mu or the IDE of your choice and create a new Python file.

2. Add the following code:

~~~ python
from gpiozero import Robot
from time import sleep

robin = Robot(left=(7,8), right=(9,10))
~~~

The first line imports `Robot`, which you will use to control the direction and speed of the motors, from the GPIO Zero library. The second line imports `sleep` from the `time` library.

The final line defines the `Robot`. You can name the variable anything you like; I've chosen to call my robot `robin`.

When initialising the `Robot` you need to give it two arguments: `left` and `right`. The `left` argument should specify the two GPIO pins on the Raspberry Pi that are connected to the pins labelled **IN1** and **IN2** on the motor controller. I chose GPIO pins 7 and 8, but yours might be different.

Similarly, the `right` argument needs to specify the GPIO pins that are connected to the pins labelled **IN3** and **IN4**; for me that is GPIO pins 9 and 10.

3. Save your file.

#### Forwards and backwards

You now need to test which direction is forwards on each motor.

4. Add this code, which will drive both motors forward, wait one second, and then stop the motors:

~~~ python
robin.forward()
sleep(1)
robin.stop()
~~~

**Note:** `robin` is the name I gave my `Robot`; if you chose a different name, make sure you change `robin`.

Run the program and check that both motors are turning in the direction of the arrows you drew.

![Video-gif of the DC motors labelled with arrows showing the direction both the motors should be spinning when the forward() command is entered](images/1_7-motors-spinning-forward)

If either motor is turning in the wrong direction, alter your program by swapping the pin numbers for that motor.

~~~ python
# for example, change the left pins from
robin = Robot(left=(7,8), right=(9,10))
# to
robin = Robot(left=(8,7), right=(9,10))
~~~

Stop the program and run it again to check how any changes you made have affected the motors.

5. Test that the motors both turn backwards by adding `robin.backward()` and another `sleep` and running your program.

~~~ python
robin.forward()
sleep(1)
robin.backward()
sleep(1)
robin.stop()
~~~

You should see both the motors turn forwards for one second and then backwards for one second before stopping.

Repeat steps 4 and 5 until both motors turn forwards and backwards correctly.

#### Left and right

Finally, you are going to test whether your program correctly identifies the left and right motors, by using the `.right()` command.

6. Add the following lines of code to your program. Run the program and note which motor changes direction on the command `robin.right(0.6)`.

~~~ python
robin.forward(0.6)
sleep(1)
robin.right(0.6)
sleep(1)
robin.stop()
~~~

**Note:** The 0.6 inside the `.forward()` and `.right()` commands makes the motors go a little slower. The default speed is 1.

The motor that changed direction is the one that your program has defined as the right-hand motor. If this matches your label, then there’s nothing to change. If this motor was the one you labelled 'left', you need to alter your `Robot` code to swap the left pin numbers with the right pins:

~~~ python
# for example, change the GPIO pins from
robin = Robot(left=(7,8), right=(9,10))
# to
robin = Robot(left=(9,10), right=(7,8))
~~~

Repeat step 6 until the motor labelled 'right' changes direction.

#### Potential problems

If you are having problems with getting the motors to turn in the correct directions, try working through this step again with a new Python file.

**Top tip:** If there is a problem with your program or the wiring, the motors can spin continuously. If this happens, try entering the command `robin.stop()` (replacing `robin` with the name you gave your robot) into the Python shell. Otherwise, turn off the battery pack or Raspberry Pi and check that the wiring is correct.

If the motors aren't moving at all, try the following:

+ Use the previous steps to check that the wiring of the components is correct
+ Check that all the connections are secure
+ Check that your battery pack is correctly filled with working batteries and is turned on

### Challenge: Experimenting with direction and speed

+ Create a Python file including each of the commands: `.forward()`, `.backward()`, `.left()`, and `.right()`

+ Experiment with giving these commands different values inside the brackets, e.g. `robin.left(0.65)`

### Discussion

Do you need any help? Share any issues you have below.
