[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Challenge: improving the obstacle avoidance

There are some limitations and improvements that could be made to the program in the previous step, which may result in a more robust solution to autonomously avoiding objects. 

### Potential improvements

You may want to experiment with different distance thresholds and sleep values to see how that affects the buggy's ability to avoid an obstacle.

Another improvement you could make to the program is to allow the buggy to randomly choose to turn left or right once an obstacle is detected. How might you program this?

Can you think of any other improvements that could be made to the program?

### Limitations of the program

You may have found that an object which is really close to the UDS returns a much larger distance than expected. This usually occurs if an object is closer than the minimum distance a UDS can detect accurately - for my UDS that's anything 2mm or less away from the sensors. Likewise, a UDS will have a maximum range it can measure accurately, which for my UDS is 500cm or half a metre. 

Take a look at the distance values that are output when an object 

How might you 


At the moment, this limitation of the sensor isn't going to affect the program massively but be aware of it incase the buggy doesn't behave as intended with really close or distant objects. You could try and find a hack to detect and respond to really close or distant objects.

Did you find a work around for an object that was too close for the UDS to measure the distance accurately?

Share your ideas and any code you create in the comments below.