[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Testing the line sensors

Now you are going to attach your line following sensors to the buggy and test whether the sensors are picking up the differences between light and dark surfaces. This is best done on a track made with white paper or card and black tape for the line - you'll  also use this later on to test the line following ability of your robot.

### What you will need

+ White paper or card (at least 3 sheets of A4)
+ Black tape (a black marker pen would also work)

You may also need:

+ Screwdriver

![Picture of the parts for building a track for the buggy and testing the line following sensors - white paper, black tape, screwdriver](images/3_6-parts-for-line-testing)

### Preparing your track

In order to test your buggy, you'll need to prepare a track with a line for the robot buggy to follow. The simple track that I made to initially to test the buggy consists of three pieces of A4 paper placed in a slightly curved row, with a single strip of black tape making a line through the middle of the paper (as pictured below). This provides a really clear contrast in light levels between the white paper and the black tape so that your line sensors are be able to accurately detect whether they are over the line or not.

![Picture of a white piece of card with a black line of tape running through the center](images/)

### Attaching the sensors to the chassis

Before you modify the chassis, I recommend taking a photo of your buggy and the connections between the Raspberry Pi, motor controller board, and Ultrasonic Distance Sensor (UDS). It is quite likely that a few of the jumper leads will come loose during this process. Use the photo of the buggy and/or the  steps in the previous 2 weeks of this course to help you check and reconnect the leads correctly.

When using two line sensors, you want them to be positioned near the front of the chassis and evenly spaced either side of the caster wheel. This is so each sensor can detect when it is over the line with minimal delay, meaning that the buggy can be programmed to change course before it has drifted too far either side of the line. The smaller the gap is between the sensors, the less the buggy will need to wiggle side-to-side before it is directly over the line again.

![Animation from 3.4](images/3_4_Two_Sensors_Anim.gif)

On the chassis, mark where you want to position the line sensors so that each sensor will be either side of the line beneath it. Cut two small holes in the bottom of your chassis so that the infrared (IR) emitter and receiver can fit through (the blue and black components that look like LEDs). You may also need to leave space for the potentiometer and/or the tiny LED (which should be labelled) to fit through if these components are on the same side as the IR emitter and receiver.

![Picture of one line sensor secured to the buggy and a hole where the other line sensor should be placed](images/)

The optimal distance between the surface and the sensor is 1cm to 3cm, which should be fine for most buggies. The sensors will be able to detect light levels at closer and further distances, though not quite as accurately, in which case you may need to adjust the sensitivity using the potentiometer.

### Tuning the line sensors

You are need to check that the line sensors can reliably detect the difference between a white surface and a black line. This may require the sensors to be tuned using the potentiometer.

With the line sensors attached, boot up your Raspberry Pi. Move the buggy slowly side to side so each of the line sensors passes over the black line.

Whilst a sensor is over a **light** surface, the LED on the sensor board should be **on**. Conversely, when a sensor passes over a **dark** line, the LED on the sensor should be **off**.

![Video-gif of the LED on each line sensor turning on when the sensor is over the white surface and off when the sensor is over the black line](images/)

If either of the sensors are not accurately picking up the changes in light between the white paper and the black line, you will need to adjust the sensitivity of the potentiometer using a screwdriver. Be careful when turning the potentiometer as it is quite a delicate component.

Ideally, the LED of each sensor should be off as soon as the black line is directly underneath it with as little delay as possible. If the potentiometer is facing the floor, you will need to adjust the potentiometer a small amount and then check whether the sensitivity of line sensor has improved or not. Repeat this process until you are happy with the reliability of both sensors.

![Picture of the potentiometer on one of the line sensors being tuned with a screwdriver](images/)
