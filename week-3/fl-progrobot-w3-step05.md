[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Connecting the line sensors

For the remainder of this week, you will turn your buggy into a line-following robot buggy. In this setup, I will be demonstrating how to connect two TCRT5000 line sensors to a Raspberry Pi. If you are not using the same line sensors the instructions may differ, so check the specifications of your sensors.

### What you will need

For this step, you will need the following items:

+ 8 female-to-female jumper leads
+ 2 line following sensors
+ Soldering iron and solder
+ Wire strippers
+ Scissors
+ Tape

**You can use the [getting started with soldering](https://projects.raspberrypi.org/en/projects/getting-started-with-soldering) resource posted in the first week for guidance, and to learn some quick tips and tricks.**

![Picture of the robot buggy parts for this step - 8 female-to-female jumper leads, 2 line following sensors, Soldering iron and solder, Wire strippers, Scissors, Tape](images/3_5-parts-for-line-sensors)

### Prepare the connectors 

For this build, I will be using two TCRT5000 line sensors which have a working voltage of 3.3V to 5V.

Some of you will only have one 5V pin free...

You are going to connect the two VCC pins (one from each sensor) to one 5V pin on the Raspberry Pi. Similarly, you are going to connect two GND pins (one from each line sensor) to one GND pin on the Raspberry Pi.


For this setup, you are going to connect two GND pins (one from each line sensor) to one GND pin on the Raspberry Pi. You are also going to connect two VCC pins (one from each sensor) to one 5V pin on the Pi. This is because...

<!-- 
Explain that we are going to connect the two GND pins of the sensor to one GND pin on the Pi - just like some of you did with the battery pack and Pi wires that connected to one GND terminal on the motor controller board.
You will also connect both of the VCC pins to one 5V pin on the Pi which will power both sensors because... 
-->

The first stage will be to connect your line sensors to your Raspberry Pi. Normally, the type of line sensor used in this project needs to be connected to a **3V3** pin, but you’re going to run two sensors via the same power pin, so you’ll attach both sensors to a **5V** pin.

Start by taking three of the female-female jumper leads and removing one of the connectors from the end of each lead with scissors. If you are using female-male jumper leads, make sure you remove the male end as you will need the female end to connect to the line sensors.

Strip the plastic sheath of the bare ends to reveal **at least** a centimeter of the multi-core wire beneath. The more exposed wire there is, the easier it is to twist the ends together.

![Picture of three female jumper leads with one end of each lead stripper - taken from project "Build a line following robot"](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/stripped.jpg)

Place two of the jumper leads side-by-side so the multi-core wires are next to each other. Turn the third lead so it is facing the opposite way to the other leads and place the exposed wires next to the wires of the other leads in the shape of a two-pronged fork. 

![Picture of three jumper leads placed together as a two-pronged fork with the exposed multi-core wires all touching each other](images/3_5-jumper-leads-2-pronged-fork)

Twist the wires of the two jumper leads that are side-by-side together first. Then wrap the wire of the third jumper lead around the other two wires. All three wires should be intertwined now. Don't worry if the wires are connected a bit loosely - you are going to solder the wires together and then wrap the connection in tape to make it extra secure. 

Heat up the soldering iron. Hold the tip of the soldering iron to the exposed multi-core wires for a few seconds, then apply the solder to the tip until it melts and bonds the bare wires with a small amount of solder. 

![Video-gif of three jumper leads with the multi-core wires twisted together being soldered together](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/solder.gif)

Let the solder cool for a minute and the wrap the join of the leads with a small amount of insulating tape.

![Picture of the three joined jumper leads with tape covering the soldered bond](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/soldered.jpg)

Repeat the entire process with another three female-to-female jumper leads.

### Connect the line sensors to the Raspberry Pi

The line sensor I am using has three pins: **VCC** for power, **GND** for ground, and **DO** for digital out. These are the only pins you will need to use for the buggy, though your line sensor may have an extra **AO** pin for analogue out.

![Diagram of a line following sensor with the pins VCC, GND and DO labelled clearly](images/)

Take one of your soldered-together three-wire jumper leads, and connect two of its ends to the **VCC** pin on each of the two sensors.

![Picture of a three-wired jumper leads connected to the VCC pin on two line following sensors](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/power.jpg)

Take the second of your soldered jumper leads, and connect two ends to the **GND** pin on each line sensor.

![Picture of the second three-wired jumper leads connected to the GND pin on two line following sensors](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/ground.jpg)

Take your remaining two single jumper leads and connect each one to the **DO** pin on each line sensors.

![Picture of the two single jumper leads connected to the DO pin on two line following sensors](https://projects-static.raspberrypi.org/projects/rpi-python-line-following/5231de01afcfc787873b5b674045505e9dad8f1c/en/images/digital_out.jpg)

Now connect the **VCC** pins of both line sensors to a **5V** pin on your Raspberry Pi, and the **GND** pins of the sensors to a **GND** pin on your Raspberry Pi. Each of the two **DO** pins can be connected to any numbered GPIO pin. In this example, pin **GPIO 16** is used for the left sensor and **GPIO 20** is used for the right sensor.

![Picture of the buggy with the two line following sensors attached to the Raspberry Pi](images/3_5-buggy-two-sensors)

Share how you got on and any other tips in the comments below.
