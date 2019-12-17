[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Testing the line sensors

Next you’re going to attach your line following sensors to the buggy and test whether the sensors are working. You will tune the line sensors a little to ensure they are picking up changes in light between white paper and a black line.

### What you will need

+ White piece of card
+ Black tape
+ Screwdriver

![Picture of the parts for building a track for the buggy and testing the line following sensors - white card, black tape, screwdriver](images/3_6-parts-for-line-sensors)

### Preparing your track 

First, you will need to prepare a line for the buggy to follow. I am going to use a white piece of card for the background surface with a black strip of tape for the line so there is a really clear contrast in light levels that the sensor can detect.

![Picture of a white piece of card with a black line of tape running through the center](images/)

### Attaching the sensors to the chassis

Next, you will need to figure out where the line sensors need to be secured to the buggy so they can follow a line effectively.

Both of the line sensors need to be positioned near the front of the chassis, with one either side of the ball caster. This way, the sensors will be able to detect whether it is directly over the line, to the left of the line, or to the right of the line. 

On the buggy, mark where you want to position the line sensors so that the sensor can view the line beneath it. Cut two small holes in the bottom of your buggy and secure the sensors in place.

<!-- include the range of distance the sensors should be from the surface before affixing it to the chassis -->

![Picture of one line sensor secured to the buggy and a hole where the other line sensor should be placed](images/)

### Tuning the line sensors

You are now going to check that the line sensors detect the difference between a light surface and a dark line.

With the line sensors attached, boot up your Raspberry Pi. Move the buggy slowly side to side so each of the line sensors passes over the dark line.

Whilst a sensor is over a light surface, the LED on the sensor board should turn off. Conversely, when a sensor passes over a dark line, the LED on the sensor should turn off.

![Video-gif of the LED on each line sensor turning on when the sensor is over the white surface and off when the sensor is over the black line](images/)

<!-- Re-write and further explain the following paragraph -->

Use the small potentiometer on the board to tune your sensors, so that the LEDs turns off when over a dark line, and lights up when over white space.

![Picture of the potentiometer on one of the line sensors being tuned with a screwdriver](images/)

Once you have tuned the sensors, you can proceed to programming your robot in the next step.