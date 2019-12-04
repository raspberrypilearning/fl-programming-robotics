[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Challenge: improving the obstacle avoidance program

There are some limitations and improvements that could be made to the program in the previous step. Make a copy of the program first, then modify the code to try and improve the robot buggy's ability to avoid objects autonomously.

### Potential improvements

You might want to start by experimenting with different distance thresholds and sleep values to see how that affects the performance of the buggy.

Another improvement you could make to the program is to allow the buggy to randomly choose to turn left or right once an obstacle is detected. **How might you code this?**

### Limitations of the buggy

You may have noticed that an object which is really close to the UDS returns a much larger distance than expected. This usually occurs if an object is closer than the minimum distance a UDS can detect accurately; for the HC-SR04 UDS the detection distance is about 2cm-500cm.

Take a look at the distance values that are output when an object is very close to the UDS and see if you can find a hack within the program to pick up these objects. 

Another possible limitation is that the UDS will not detect objects either side of it, which the buggy may hit if the chassis is wider than the range of the UDS. A solution to this could be to add an extra UDS to the front of the buggy and have a UDS either side of the chassis.

**Can you think of any other limitations or improvements that could be made to the program?**

**What improvements are you going to make to the program?**

**Did you find a solution to the UDS not picking up objects that are really close to it?**

Share your ideas and any programs that you modify in the comments below.