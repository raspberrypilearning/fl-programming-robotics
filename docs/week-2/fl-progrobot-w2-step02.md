[comment]: # (
Feedback Author: Normally lead educator
)

## Quiz: Mobile robotics

Last week, you learnt about some of the different components that you can use to build a robot buggy. 

In this quiz, you will test your knowledge of how these components connect and work together to create a mobile robot.

### Question 1

Which of these things can nearly all robots do?

+ Think, learn, and act
    + No
    + Many robots aren't able to learn; instead, they perform actions based on written instructions
    + Week 1, step 3
+ Sense, process, and learn
    + No
    + Many robots aren't able to learn; instead, they perform actions based on written instructions
    + Week 1, step 3
+ Think, process, and learn
    + No
    + Many robots aren't able to think or learn; instead, they perform actions based on written instructions
    + Week 1, step 3
+ Sense, process, and act
    + Yes
    + N/A
    + Week 1, step 3

### Question 2

What is the maximum input voltage that a Raspberry Pi can handle through the GPIO pins?

+ 3V
    + No
    + A Raspberry Pi can handle input voltages higher than 3V from the GPIO pins
    + Week 1, step 4
+ 3.3V
    + Yes
    + N/A
    + Week 1, step 4
+ 5V
    + No
    + An input voltage of 5V is too high for a Raspberry Pi to handle through the GPIO pins and will damage it
    + Week 1, step 4
+ 5.5V
    + No
    + An input voltage of 5.5V is too high for a Raspberry Pi to handle through the GPIO pins and will damage it
    + Week 1, step 4

### Question 3

When testing the movement of your robot buggy, why do you need to perform the `.stop()` command before closing the Python program? 

+ This switches the motor controller board off so it doesn’t use any more power
    + No
    + The motor controller will still draw power until the battery pack and/or the Raspberry Pi is switched off
    + Week 1, step 7
+ Otherwise the motors will continue to spin in the direction they have been instructed to
    + Yes
    + N/A
    + Week 1, step 7
+ If the robot isn’t instructed to stop first, the program will output an error
    + No
    + Not including the `.stop()` command before closing the program won't cause an error in Python
    + Week 1, step 7
+ So that the Raspberry Pi and the motors are shut down safely
    + No
    + The `.stop()` command in GPIO Zero is for controlling the motors, not the motor controller or the Raspberry Pi
    + Week 1, step 7

### Question 4

Which series of commands could be used to instruct a robot buggy to move in an L shape?

+ `robin.forward()`, `sleep(0.5)`, `robin.left(0.8)`, `sleep(0.5)`, `robin.forward()`
    + Yes
    + N/A
    + Week 1, step 7
+ `robin.forward(10)`, `sleep(0.5)`, `robin.left(90)`, `sleep(0.5)`, `robin.forward(10)`
    + No
    + The commands `.forward()` and `.left()` can only accept values from a range of -1 to 1
    + Week 1, step 7
+ `robin.left(0.8)`, `sleep(0.5)`, `robin.forward()`, `sleep(0.5)`, `robin.left(0.8)`
    + No
    + This algorithm would need an extra `sleep()` and `.forward()` command at the end for it to make an L shape
    + Week 1, step 7
+ `robin.left(90)`, `sleep(0.5)`, `robin.forward(10)`, `sleep(0.5)`, `robin.left(90)`
    + No
    + The commands `.forward()` and `.left()` can only accept values from a range of -1 to 1
    + Week 1, step 7
