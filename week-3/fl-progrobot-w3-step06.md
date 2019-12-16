[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Connecting the line sensors

For the remainder of this week, you will turn your buggy into a line-following robot buggy. To start with, you need to connect 2 line following sensors to the Raspberry Pi.

### What you will need

For this step, you will need the following items:

+ 8 female-to-female or female-to-male jumper leads
+ 2 line following sensors
+ Soldering iron and solder
+ Wire strippers
+ Scissors
+ Tape

**You can use the [getting started with soldering](https://projects.raspberrypi.org/en/projects/getting-started-with-soldering) resource posted in the first week for guidance, and to learn some quick tips and tricks.**

![Picture of the robot buggy parts for this step - 8 female-to-female jumper leads, 2 line following sensors, Soldering iron and solder, Wire strippers, Scissors, Tape](images/3_6-parts-for-line-sensors)

### Prepare the connectors

The first stage will be to connect your line sensors to your Raspberry Pi. Normally, the type of line sensor used in this project needs to be connected to a **3V3** pin, but you’re going to run two sensors via the same power pin, so you’ll attach both of sensors to a **5V** pin.

Start by taking three of the female-female jumper leads and removing one of the connectors from the end of each lead with scissors. If you are using female-male jumper leads, make sure you remove the male end as you will need the female end to connect to the line sensors. 

Strip the plastic sheath of the bare ends to reveal about a centimeter of the multi-core wire beneath.

![Picture of three female jumper leads with one end of each lead stripper - taken from project "Build a line following robot"](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/stripped.jpg)

Place two of the jumper leads side-by-side so the multi-core wires are next to each other. Turn the third lead so it is facing the opposite way to the other leads and place the exposed wires next to the wires of the other leads in the shape of a two-pronged fork. Take all three jumper leads and twist their multi-core wires together. Then use a soldering iron to bond the leads.

![Video-gif of three jumper leads with the multi-core wires twisted together being soldered together](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/solder.gif)

Cover the join of the leads with a small amount of insulating tape.

![Picture of the three joined jumper leads with tape covering the soldered bond](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/soldered.jpg)

Repeat the entire process with another three female-to-female jumper leads.

### Connect the line sensors to the buggy

Most line sensors have three pins: **VCC** for power, **GND** for ground, and **DO** for digital out.

![Picture of a line following sensor with the pins VCC, GND and DO labelled clearly](images/)

Take one of your soldered-together three-wire jumper leads, and connect two of its ends to the **VCC** pin on each of the two sensors.

![Picture of a three-wired jumper leads connected to the VCC pin on two line following sensors](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/power.jpg)

Take the second of your soldered jumper leads, and connect two ends to the **GND** pin on each line sensor.

![Picture of the second three-wired jumper leads connected to the GND pin on two line following sensors](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/ground.jpg)

Take your remaining two single jumper leads and connect each one to the **DO** pin on each line sensors.

![Picture of the two single jumper leads connected to the DO pin on two line following sensors](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/digital_out.jpg)

Now connect the **VCC** pins of both line sensors to a **5V** pin on your Raspberry Pi, and the **GND** pins of the sensors to a **GND** pin on your Raspberry Pi. Each of the two **DO** pins can be connected to any numbered GPIO pin. In this example, pins **GPIO 6** and **GPIO 12** are used.

![Picture of the buggy with the two line following sensors attached to the Raspberry Pi](images/3_6-buggy-two-sensors)

Share how you got on and any other soldering tips in the comments below.