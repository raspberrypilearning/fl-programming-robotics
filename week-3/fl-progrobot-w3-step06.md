[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Testing the line sensors

Now you are going to attach your line following sensors to the buggy and test whether the sensors are picking up the differences between light and dark surfaces. This is best done on a track that you will use later to test the line following ability of your robot, which you will make with white paper and black tape.

### What you will need

+ White paper or card (3 sheets of A4 minimum)
+ Black tape
+ Screwdriver

![Picture of the parts for building a track for the buggy and testing the line following sensors - white card, black tape, screwdriver](images/3_6-parts-for-line-testing)

### Preparing your track 

To start with, you will need to prepare a line for the robot buggy to follow. The simple track I made to initially to test the buggy consisted of three pieces of A4 paper placed in a slightly curved row with a single strip of black tape making a line through the middle of the paper, as pictured below. This provides a really clear contrast in light levels between the white paper for the background surface and the black tape for the line that the line sensors should be able to detect accurately. 

![Picture of a white piece of card with a black line of tape running through the center](images/)

### Attaching the sensors to the chassis

<!-- DELETE --> Next, you will need to figure out where the line sensors need to be secured to the buggy so they can follow a line effectively.

Before you do this, I recommend taking a photo of your buggy and the connections between the Raspberry Pi, motor controller board, and UDS. It is quite likely that a few of the jumper leads will come loose during this process. Use the photo of the buggy and/or the building the buggy steps in the previous 2 weeks of this course to help you check and reconnect the leads correctly.

Both of the line sensors need to be positioned near the front of the chassis, with one either side of the ball caster. This way, the sensors will be able to detect where the buggy is in relation to the line.

The sensors should also be placed fairly close to the center of the chassis, not towards the far left or far right of the buggy if possible. This is because the algorithm you will program is written so that the buggy will move forwards when no line is detected, or left or right depending on which sensor detects the line. Therefore, the smaller the gap is between the sensors, the less the buggy will wiggle side-to-side before it is directly over the line again. 

![Animation from 3.4](images/)

On the chassis, mark where you want to position the line sensors so that each sensor is either side of the line beneath it. The optimal distance between the surface and the sensor is 1cm to 3cm, which should be fine for most buggies. The sensors will be able to detect light levels at closer and further distances, though not quite as accurately, in which case you may need to attach them to the ??bonnet?? of the buggy.

Cut two small holes in the bottom of your buggy so that the infrared (IR) emitter and receiver can fit through (the blue and black components that look like LEDs). You may also need to leave space for the potentiometer and/or the tiny LED (which should be labelled) to fit through if these components are on the same side as the IR emitter and receiver.

![Picture of one line sensor secured to the buggy and a hole where the other line sensor should be placed](images/)

### Tuning the line sensors

You are now going to check that the line sensors detect the difference between a light surface and a dark line.

With the line sensors attached, boot up your Raspberry Pi. Move the buggy slowly side to side so each of the line sensors passes over the dark line.

Whilst a sensor is over a **light** surface, the LED on the sensor board should be **on**. Conversely, when a sensor passes over a **dark** line, the LED on the sensor should be **off**.

![Video-gif of the LED on each line sensor turning on when the sensor is over the white surface and off when the sensor is over the black line](images/)

You may need to tune the line sensors a little to ensure they are accurately picking up changes in light between the white paper and black line. To fine tune the sensors, you can adjust the sensitivity of the potentiometer with a screwdriver. Be careful if you do use a screwdriver as the potentiometer is quite a delicate component. Ideally, the LED of each sensor should be off as soon as the black line is directly underneath it.

If the potentiometer is facing the floor, you will need to adjust the potentiometer a small amount and then check whether the line sensor has improved at detecting the black line and the white surface. Repeat this until you are happy with the sensitivity of both sensors.

![Picture of the potentiometer on one of the line sensors being tuned with a screwdriver](images/)