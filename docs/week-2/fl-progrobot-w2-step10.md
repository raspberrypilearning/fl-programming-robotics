## Challenge: Improving the obstacle-avoidance program

There are a number of modifications that will improve your robot's ability to avoid objects autonomously. Most of these require changes to the program from the previous step.

First, I suggest making a copy of your program before modifying any of the code, in case something you try doesn't work out.

### Changing some of the values

Begin by experimenting with different distance thresholds and sleep values, to see how that affects the performance of the robot.

For example, the distance threshold of 0.2 metres used in the previous program may need to be increased slightly if your robot does not start to turn out of the way of an obstacle in time.

You can also change the sleep value of 0.5 seconds, so that the robot continues turning for more or less time once the threshold value has been met.

### Changing the robot's behaviour

Currently, the robot turns left for a set amount of time whenever an object is detected as being too close.

This predictable behaviour has the potential to cause issues. One problem is that the robot might get stuck in an obstacle avoidance loop when turning by a fixed amount each time. In this situation, the robot keeps detecting the same obstacles over and over again, seemingly with no way to escape!

There are a number of changes you can make to the robot's behaviour.

#### Two steps forward, one step back

One modification you can make is to instruct the robot to move backwards for a period of time before turning to avoid an object. This will give your robot a chance to avoid obstacles if it has found itself in a dead end.

Another solution is to introduce random aspects into the robot's movements. For example, you could import the `random` library into your Python program and use the function `random.randint(0,1)` to return a random integer that's either 0 or 1. How might you adapt your program so it chooses a direction based on this random value?

#### Randomising the amount of time the robot turns

Rather than turning left for a set amount of time, you can instruct the program to generate a random number of seconds within a certain range of values.

To add this functionality, you will need to import the `random` library into your Python program. Use the function `random.uniform(a, b)` to return a random floating-point number, where `a` is the lowest value and `b` is the highest value.

#### Choosing a random direction

Another modification to the robot's behaviour is to allow the program to choose a random direction to turn once an obstacle has been detected. Instead of always turning left, the robot could be instructed to turn *either* left or right. How might you code this?

### Limitations of the UDS

There are some limitations it is important to be aware of when using a UDS. Finding workarounds to these problems will ensure that your program is robust.

#### Objects that are too close

You may have noticed that an object that is really close to the UDS returns a much larger distance than expected. This occurs if an object is closer than the minimum distance a UDS can detect accurately; for the HC-SR04 and HC-SR04P models, the detection distance is from about 2 cm to 500 cm.

Take a look at the distance values that are output when an object is very close to the UDS and see if you can find a solution within the program to pick up these objects.

#### Objects that are to the side

Another issue that your robot may run into is that, depending on the width of your robot, the UDS won't detect objects on either side of it that are going to be in the way.

One solution to this would be to add an extra UDS to the front of the robot, so that there is one on each side of the chassis. This modification would also require the program to be adapted so that it is able to work with two UDSs.

### What improvements will you make?

Improve your program using one of the ideas in this step:

- Change the distance threshold and/or sleep values
- Once your robot has detected an obstacle:
    - Instruct it to move backwards before turning left
    - Generate a random number of seconds for the robot to turn for
    - Get the program to choose a random direction for the robot to turn in
- Find a solution for detecting objects that are closer than the minimum detection distance of your UDS
- Attach another UDS to the chassis and modify your program so it works with two UDSs

### Discussion

Can you think of any other improvements that you could make?

In the comments below share the changes you made and your new code.

Remember to use three tilde characters (`~~~`) at the start and end of your code, as in this example comment text:

<pre><code>I created this program.

~~~
print("This is my code")
~~~
</code></pre>

Refer to our ['Sharing code on FutureLearn' guide](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/all+courses+/Sharing+code+on+FutureLearn.pdf) for more information.
