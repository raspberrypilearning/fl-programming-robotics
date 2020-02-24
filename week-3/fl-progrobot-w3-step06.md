[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Testing the line sensors

You are now going to attach your line-following sensors to the chassis and test whether they are picking up the difference between light and dark surfaces.

### What you will need

+ White paper or card (at least three sheets of A4)
+ Black tape (a black marker pen would also work)

You may also need:

+ A screwdriver

![Picture of the parts for building a track for the robot and testing the line following sensors - white paper, black tape, screwdriver](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/3_6-parts_for_line_testing.jpg)

### Preparing your track

To test your robot, you'll need to prepare a track with a line for it to follow. I made a simple track out of three pieces of A4 paper placed in a slightly curved row, with a single strip of black tape making a line through the middle of the paper, as pictured below.

![Picture of a three white pieces of paper joined in a curve with a black line of tape running through the center](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/3_6-black_line_on_white_paper.jpg)

This provides a clear contrast in light levels between the white paper and the black tape, so your line sensors should be able to detect accurately when the line is beneath them.

### Attaching the sensors to the chassis

Before you modify the chassis, I recommend taking a few photos of your robot and the connections between the pins on the Raspberry Pi and the components. It is quite likely that a few of the jumper leads will come loose while you are attaching the line sensors to the chassis. You can use the photo of the robot, and/or the steps covered in the previous two weeks of this course, to help you check the leads and reconnect them correctly if necessary.

#### Positioning the line sensors

When using two line sensors, you want them to be positioned near the front of the chassis, and evenly spaced on either side of the caster wheel. This is so that each sensor can detect when it is over the line with minimal delay, so that the robot can be programmed to change course before it has drifted too far to either side of the line. The smaller the gap is between the sensors, the less the robot will need to wiggle from side to side before it is positioned directly over the line again.

![Top down animation a robot buggy following a black line. The buggy moves forwards and turns right if the right sensor detects the line, and turns left if the left sensor detects the line.](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Animation/3_4-line-following-buggy-animation.gif)

The optimal distance between the surface and the sensor is from 1 cm to 3 cm, which should be fine for most chassis. If not, you may need to tune the sensors later, using the instructions below.

Align your robot so that the centre of the robot is directly over the black line on your track. On the chassis, mark where you want to position the line sensors so that the sensors will be on either side of the line.

#### Securing the sensors to the chassis

Cut two small holes in the bottom of your chassis so that the infrared (IR) emitter and receiver (the blue and black components that look like LEDs) can fit through. If the potentiometer and/or the tiny LED (which indicates when a line has been detected) are on the same side as the IR emitter and receiver, you will also need to include some space for these to fit through. Ideally, the holes will be big enough so that these parts can fit through them without the entire sensor dropping through the hole!

![Picture of one line sensor in place on the chassis and a hole where the other line sensor should be placed](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/3_6-one_line_sensor_in_place.jpg)

You can then secure the sensor in place using tape; make sure the tape doesn't cover the IR emitter or receiver.

### Tuning the line sensors

You are need to check that the line sensors can detect the difference between a white surface and a black line reliably, and tune them up using the potentiometer.

With the line sensors attached, boot up your Raspberry Pi. Move the robot slowly from side to side so that each of the line sensors passes over the black line.

When a sensor is over a **light** surface, the LED on the sensor board should be **on**. Conversely, when a sensor passes over a **dark** line, the LED on the sensor should be **off**.

Ideally, the LED of each sensor should be off as soon as the black line is directly underneath it, with as little delay as possible. If either of the sensors is not picking up the changes in light between the white paper and the black line accurately, you will need to adjust the threshold value by adjusting the potentiometer using a screwdriver. Be careful when turning the potentiometer, as it is quite a delicate component.

![Picture of the potentiometer on one of the line sensors being tuned with a screwdriver](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/3_6-potentiometer-tuning.jpg)

### Discussion

How did you get on with testing the line sensors? Did you have any issues? Share your thoughts in the comments.

In the next step you will have an opportunity to reflect on how you have got on in the course so far.
