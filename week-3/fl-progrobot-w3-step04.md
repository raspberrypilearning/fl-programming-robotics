[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Line sensors and how to use them

In this step you will investigate how the specific line sensor you will be using (the TCRT5000 IR sensor) works and how it detects a line. This knowledge will help you design and program a line following algorithm later in the week. 

### IR detection

Line sensors detect the presence of either a black or white line by emitting infrared (IR) light and detecting the light levels that return to the sensor. It does so using 2 components - an emitter and a light sensor (receiver).

![](https://www.aam.com.pk/wp-content/uploads/2017/09/tcrt5000.jpg)

In the picture above you can see these 2 components that look like LEDs on the bottom (right hand side). The black one is the IR emitter and the "blue" one is the receiver. These devices also have a **potentiometer** on them that can be used to adjust the sensitivity - this is the blue box on the left hand side of the image above. The central white section can be turned with a screwdriver to change the sensitivity.

The sensor will emit IR light and the sensor will measure the light level that is reflected from the surface underneath. Most line sensors have 2 types of output - analogue and digital. The analogue output will return a constant reading of the light levels the sensor is detecting, but analogue input does not work on the Raspberry Pi. The digital output will compare the value to the sensitivity set by the potentiometer. If the sensor is not receiving enough light to surpass the sensitivity value, the digital output will be high (1). If enough light is received and the sensitivity value surpassed - the pin will be set to low (0). 

The setup of these devices may seem a bit backwards at first, "the pin is on when the light levels are low", but when you consider that the sensor is designed to detect black lines - it makes a bit more sense. If the IR light shines on the black line, not much light will be reflected back to the sensor and the digital pin will read high (1). If the robot then moves and the IR light is shining on white, lots of light will return to the sensor and the reading will turn low (0). This is why the output is setup in this way, so a black line will return a 1.

### How to use a line sensor. 

Now that you know a bit more about the functionality of a line sensor - you should also know how to use one!

The line sensor also has an array of pins that you will have to connect to the Pi you are using, they are;

+ `VCC` is the pin used to power the device, it will accept anything between 3.3V and 5V
+ `GND` is the ground pin and is required to complete the circuit
+ `A0` is the analogue output (will not work with a Pi)
+ `DO` is the digital output pin (this will work with the Pi)

The VCC pin here can take a range of voltages so potential dividers are not necessary. 

### Just one sensor won't do. 

Whilst one sensor will tell you whether there is a line underneath it or not - this information alone is not enough for the robot to *follow* a line.  When the robot loses the line the robot will have no idea which way the line went - and cannot correct it's course to find the line again. 

To solve this problem, you have to use more than 1 sensor. If you add a second sensor, and spread them out so they are evenly spaced either side of the caster wheel, the information from both sensors will allow your robot to follow a line. 

Let's assume you are using a black line on a white background. If the line is in the centre of the robot then both sensors will return a 0 from their digital pins, as they are both over the white background. 

![](images/3_4_Two_Sensors_Still.png)

However, if the robot moves to the right then the left sensor will eventually cross onto the line - changing it's output to a 1. When this happens the robot corrects it's course and turns left. Once the sensor returns to a 0 value, we know the line is back in the middle of the bot.

The same applies when the robot turns too far left, the right sensor will move over the line and change it's reading. The robot will then turn right to correct. 

![](images/3_4_Two_Sensors_Anim.gif)

### Even more sensors

You can use even more than 2 sensors if you want, some designs use 3 or 4. 

**What would the detection and correction algorithm be for a robot with 3 sensors?**

Share your thoughts in the comments section.