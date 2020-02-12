[comment]: # (
Feedback Author: Normally lead educator
)

## Quiz: how do distance sensors work?

You have been learning about the functionality of a UDS this week, and have seen some examples of how these can be used for detecting objects.

In this quiz, you will be able to test your knowledge of how a UDS functions.

#### Question 1

What does a UDS use to measure the time it takes for an object to be detected? 

#### Choices 

+ Sound
    + No 
    + It uses a specific type of sound that humans can't typically hear. 
    + Week 2, step 6
+ Ultrasound
    + Yes 
    + N/A 
    + Week 2, step 6
+ Light
    + No
    + A UDS doesn't use light to measure the disance of objects.
    + Week 2, step 6
+ Ultraviolet light
    + No
    + A UDS doesn't use ultraviolet light to measure the disance of objects.
    + Week 2, step 6

#### Question 2

Which one of these is an advantage of a UDS over other types of distance sensors?

#### Choices 

+ It is much more compact than most other distance sensors
    + No 
    + Different types of distance sensors can come in a range of sizes depending on factors such as the range of the sensor.
    + Week 2, step 6
+ It is quicker at calculating the time taken for a signal to be emitted and received 
    + No 
    + A UDS is not quicker at calculating the time taken to reflect back from an object than some other types of distance sensors that use light.
    + Week 2, step 6
+ It is not effected by sound waves that interfere with the signal
    + No
    + A UDS signal can be disrupted by certain sound waves.
    + Week 2, step 6
+ It is not effected by the colour of the object that the signal reflects off
    + Yes
    + N/A
    + Week 2, step 6

#### Question 3

What happens if an object is closer than the **minimum** range of the UDS?

#### Choices 

+ A large value is output by the sensor
    + Yes 
    + The receiver might not pick up the sound when it is initially reflected off an object, and instead detect the sound once it has rebounded off another object. This results in a higher distance reading than is accurate.
    + Week 2, step 6
+ A very small value is output by the sensor
    + No 
    + The receiver might not pick up the signal when it is initially reflected off an object, and instead detect the signal once it has rebounded off another object. 
    + Week 2, step 6
+ The sensor doesn’t output anything
    + No
    + The UDS will always output a duration even if it does not detect an object.
    + Week 2, step 8
+ An error occurs in the Python program
    + No
    + The GPIO Zero library will output a value each time the UDS is triggered.
    + Week 2, step 8

#### Question 4

What happens if an object is further away than the **maximum** range of the UDS?

#### Choices 

+ A large value is output by the sensor
    + Yes 
    + If the receiver doesn’t detect the ultrasound after a set time, the Echo pin returns to low. This duration indicates that no objects were detected within the maximum range of the sensor.
    + Week 2, step 8
+ A very small value is output by the sensor
    + No 
    + The receiver might not pick up the signal when it is initially reflected off an object, and instead detect the signal once it has rebounded off another object. 
    + Week 2, step 6
+ The sensor doesn’t output anything
    + No
    + The UDS will always output a duration even if it does not detect an object.
    + Week 2, step 8
+ An error occurs in the Python program
    + No
    + The GPIO Zero library will output a value each time the UDS is triggered.
    + Week 2, step 8
