[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Connecting the line sensors

The rest of this week will be spent turning your robot buggy into a line-following robot. I will be demonstrating how to connect two TCRT5000 line sensors to a Raspberry Pi. If you are not using the same line sensors, the instructions may be different, so check the specifications of your sensors.

### What you will need

You will need the following items for this step:

+ A robot buggy
+ Six female-to-female jumper leads
+ Two line-following sensors

![The robot buggy parts for this step - robot buggy, 6 female-to-female jumper leads, 2 line following sensors](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/3_5-parts-for-line-sensors.jpg)

### Making sense of your sensors

For this build, I will be using two TCRT5000 line sensors, which have a working voltage of 3.3V to 5V. This means that each line sensor can be powered from either the 5V or 3V3 pins on a Raspberry Pi.

The power pins that you have free will depend on the set-up of your robot. If you don't have enough power pins available, you can remove the power pin to the ultrasonic distance sensor (UDS) for now.

The line sensor I am using has three pins: **VCC** for power, **GND** for ground, and **OUT** or **DO** for digital out (as described in the previous step). These are the only pins you will need to use for the buggy, though your line sensor may also have an extra pin for analogue out.

![Diagram of a line following sensor with the pins VCC, GND and OUT labelled clearly](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Illustration/36-3_4_TCRT_Sensor_Diagram.png)

One of the sensors will be used to detect a line on the left-hand side of the robot, and the other to detect a line on the right-hand side. Choose which sensor you want to be on the left and which on the right, before connecting them to the Raspberry Pi. Ideally, you don't want too many jumper leads crossing each other, or it can become a bit of a tangle!

### Connect the sensors to the Raspberry Pi

1. Take one of the line sensors and three female-to-female jumper leads. Connect a jumper lead to each of the **VCC**, **GND**, and **OUT** (or **DO**) pins.

![A line following sensor with the pins VCC, GND and OUT labelled clearly](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/3_5-line-sensor-three-wires.jpg)

2. Connect the jumper lead from the **VCC** pin on the line sensor to either a 3V3 or 5V pin on the Raspberry Pi.

3. Connect the **GND** pin on the sensor to a **GND** pin on the Raspberry Pi.

4. The **OUT** pin can be connected to any numbered GPIO pin. In this example, I've used **GPIO 19** for the left sensor and **GPIO 26** for the right sensor.

Repeat this process for the second line sensor, so that both sensors are connected to the Raspberry Pi.

### Discussion

If you had any issues, leave a comment below and one of the facilitators will be able to help you.
