[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Connecting the line sensors

During the remainder of this week, you will turn your robot buggy into a line-following robot. In this setup, I will be demonstrating how to connect two TCRT5000 line sensors to a Raspberry Pi. If you are not using the same line sensors the instructions may differ, so check the specifications of your sensors.

### What you will need

For this step, you will need the following items:

+ Robot buggy
+ 6 female-to-female jumper leads
+ 2 line following sensors

![Picture of the robot buggy parts for this step - robot buggy, 6 female-to-female jumper leads, 2 line following sensors](images/3_5-parts-for-line-sensors)

### Making sense of your sensors

For this build, I will be using two TCRT5000 line sensors which have a working voltage of 3.3V to 5V.

This means that each line sensor can be powered from either the 5V or 3V3 pins on a Raspberry Pi. The power pins that you have free depend on your robot setup. If you don't have enough power pins available, you can remove the power pin to the Ultrasonic Distance Sensor (UDS) for now.

The line sensor I am using has three pins: **VCC** for power, **GND** for ground, and **DO** for digital out (as described in the previous step). These are the only pins you will need to use for the buggy, though your line sensor may have an extra **AO** pin for analogue out.

![Diagram of a line following sensor with the pins VCC, GND and DO labelled clearly](images/)

One of the sensors will be used to detect a line on the left side of the robot, whilst the other sensor will detect a line on the right. Choose which sensor you want to be on the left and the right side before connecting them to the Pi. Ideally, you don't want too many of the jumper leads crossing each other, otherwise it can become a bit of a tangle!

### Connect the sensors to the Raspberry Pi

Take one of the line sensors and three female-to-female jumper leads. Then connect a jumper lead to each of the **VCC**, **GND**, and **DO** pins.

![Picture of a line sensor with three female-to-female jumper leads connected to the VCC, GND, and DO pins](images/)

Connect the jumper lead from the **VCC** pin on the line sensor to either a 3V3 or 5V pin on the Raspberry Pi.

Then connect the **GND** pin on the sensor to a **GND** pin on the Pi.

The **DO** pin can be connected to any numbered GPIO pin. In this example, I've used **GPIO 19** for the left sensor and **GPIO 26** for the right sensor.

Repeat this process for the second line sensor so that both sensors are connected to the Raspberry Pi.

![Picture of the buggy with the two line following sensors attached to the Raspberry Pi](images/3_5-buggy-two-sensors)

If you had any issues, leave a comment below and one of the facilitators will be able to help you.
