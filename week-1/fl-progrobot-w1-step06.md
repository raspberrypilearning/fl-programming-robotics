[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Connecting the Raspberry Pi and battery pack to the motor board

Now that you have attached the motors to the motor controller board, your next step is to connect the motor board to  the GPIO pins on the Raspberry Pi, and to the battery back. This will allow you to power the motor board and control the motors using the Raspberry Pi.

### What you will need

For this step you will need the following items:

+ Motor controller board (wired up to the motors)
+ Raspberry Pi
+ AA battery holder (for 4 x AA batteries)
+ 4 x AA batteries
+ Jumper leads (female-female)
+ Screwdriver

You may also need:

+ GPIO reference card

### Connect the battery pack to the motor board

The motors require more power than the Raspberry Pi can provide. Therefore, you will use 4 AA batteries to power them.

The battery pack should include 2 wires, one red and one black. The red wire is the power input and needs to be inserted into the **VCC** terminal block. Some motor boards do not have a **VCC** block so instead use the voltage in block labelled **+12V**.

[comment]: # (
Mention the +5V block can be used to power another device, such as Arduino? Is the voltage too high for a Raspberry Pi?
)

The black wire is the ground wire and must be inserted into the **GND** terminal to complete the circuit for the battery pack. Make sure all the screws of the terminal blocks are tightened securely.

Insert the 4 AA batteries into the battery pack. Some battery packs have a switch to turn it on and off; if it does than turn it on. Most motor controllers have a red LED that lights up to indicate it is powered on. If the LED is not lit up, the wires may not be connected properly. You may also need new batteries or your battery pack may need to be filled completely for it to work (e.g. if it has space for 8 batteries, then insert 8 batteries).

### Receiving input

These instructions are for a "L298N Dual H Bridge DC Stepper Motor Driver Controller Board", and they will be pretty similar for most motor controller boards. Other boards may connect differently to the one that I'm using, and some boards can simply be placed onto the Raspberry Pi GPIO pins as a HAT. Check the documentation for your board if you are using a different one.

On this motor controller board there are pins labelled **IN1**, **IN2**, **IN3**, and **IN4**. Some motor boards also have one or two **GND** (ground) pins next to the **IN** pins but this board does not.

Which GPIO pins on your Pi that you use is up to you - in this part of the project, I have used **GPIO 7**, **8**, **9**, and **10**. However, if you use different GPIO pins then make sure you remember which ones they are as you will need to refer to them in the code.

Use five female-to-female jumper leads to connect the Raspberry Pi GPIO pins to the pins on the motor controller board. Each of your DC motors will need to need to use two **IN** pins to connect to the Raspberry Pi so it can turn in both directions, as well as one **GND** pin to complete the circuit.

| GPIO pin   | connects to   | board pin   |
|:----------:|:-------------:|:-----------:|
|7           |<–>            |IN1          |
|8           |<–>            |IN2          |
|9           |<–>            |IN3          |
|10          |<–>            |IN4          |
|GND         |<–>            |GND          |

If your motor board does not have a **GND** pin then you can use the terminal block that the battery pack also uses. Strip the end of the female-to-female or female-to-male wire and secure it into the **GND** terminal block that your battery pack feeds into. There will now be two wires fed into the **GND** block: one from the battery pack and one from the Raspberry Pi.

![The four In pins from the motor controller board connected to four GPIO pins on the Raspberry Pi as well as the GND pins connected from the board to the Pi.](images/)

### Powering the Pi

The Raspberry Pi will need its own source of power. A small USB power bank is the easiest way to power the Raspberry Pi as it is light and mobile. You could also make your own power bank though that is beyond the scope of this course.

For testing purposes, the Raspberry Pi can be plugged directly into the mains power supply. However, when you come to building the body of the buggy and making it move then the Pi will need a mobile source of power otherwise it won't be able to travel far from the mains power supply.

### Setting up your Pi

You should already be familiar with setting up a Raspberry Pi and using it. If not, follow this guide on [Getting started with Raspberry Pi](https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started).

The programming language I will be using in this course is **Python** together with a library called [**GPIO Zero**](https://gpiozero.readthedocs.io/en/stable/index.html), which provides an accessible way to control components through the GPIO pins. 

Python and GPIO Zero will be installed by default if your Pi is running the **Raspbian** operating system. Follow this guide on [Installing GPIO Zero](https://gpiozero.readthedocs.io/en/stable/installing.html) if you are using **Raspbian Lite** or other operating systems.

**Did you have any problems connecting the motor board to the Raspberry Pi or to the battery pack?**

**What type of power supply are you using for the Raspberry Pi?**

Answer both of these questions in the  comments section below.
