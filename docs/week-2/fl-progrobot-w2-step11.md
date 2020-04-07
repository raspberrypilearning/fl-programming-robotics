[comment]: # (
Feedback Author: Normally lead educator
)

## Quiz: How do distance sensors work?

You have been learning about the functionality of a UDS this week, and have seen some examples of how one can be used for detecting objects.

You will be able to test your knowledge of how a UDS functions in this quiz.

### Question 1

What does a UDS use to measure the time it takes for an object to be detected? 

#### Choices 

+ Radar
    + No 
    + Radar uses radio waves to detect objects but a UDS does not
    + Week 2, step 6
+ Ultrasound
    + Yes 
    + N/A 
    + Week 2, step 6
+ Infrared light
    + No
    + An infrared distance sensor uses infrared light to measure the distance of an object but a UDS does not
    + Week 2, step 6
+ Ultraviolet light
    + No
    + An  UDS doesn't use ultraviolet light to measure the distance of objects
    + Week 2, step 6

### Question 2

Which one of these is an advantage of a UDS over other types of distance sensor?

#### Choices 

+ It is much more compact than most other distance sensors
    + No 
    + Different types of distance sensor can come in a range of sizes, depending on factors such as the range of the sensor
    + Week 2, step 6
+ It is quicker at calculating the time taken for a signal to be emitted and received 
    + No 
    + A UDS is not quicker at calculating the time taken for a signal to be emitted and received than some other types of distance sensor that use light
    + Week 2, step 6
+ It is not affected by sound waves that interfere with the signal
    + No
    + A UDS signal can be disrupted by certain sound waves
    + Week 2, step 6
+ It is not affected by the colour of the object that the signal reflects off
    + Yes
    + N/A
    + Week 2, step 6

### Question 3

What happens if an object is closer than the **minimum** range of the UDS?

#### Choices 

+ A large value is output by the sensor
    + Yes 
    + The receiver may not pick up the sound when it is initially reflected off an object, and instead may detect the sound once it has rebounded off another object; this results in an inaccurately high distance reading
    + Week 2, step 6
+ A very small value is output by the sensor
    + No 
    + The receiver may not pick up the signal when it is initially reflected off an object, and instead may detect the signal once it has rebounded off another object
    + Week 2, step 6
+ The sensor doesn’t output anything
    + No
    + The UDS will always output a duration, even if it does not detect an object
    + Week 2, step 8
+ An error occurs in the Python program
    + No
    + The GPIO Zero library will output a value each time the UDS is triggered
    + Week 2, step 8

### Question 4

What happens if an object is further away than the **maximum** range of the UDS?

#### Choices 

+ A large value is output by the sensor
    + Yes 
    + If the receiver doesn’t detect the ultrasound after a set time, the Echo pin returns to low; this duration indicates that no objects were detected within the maximum range of the sensor
    + Week 2, step 8
+ A very small value is output by the sensor
    + No 
    + The receiver may not pick up the signal when it is initially reflected off an object, and may instead detect the signal once it has rebounded off another object
    + Week 2, step 6
+ The sensor doesn’t output anything
    + No
    + The UDS will always output a duration, even if it does not detect an object
    + Week 2, step 8
+ An error occurs in the Python program
    + No
    + The GPIO Zero library will output a value each time the UDS is triggered
    + Week 2, step 8
