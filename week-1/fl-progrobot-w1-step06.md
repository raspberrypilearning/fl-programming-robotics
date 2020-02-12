[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Connecting the Raspberry Pi and battery pack to the motor board

Your next step is to connect the motor board to the GPIO pins on the Raspberry Pi, and to the battery pack. This will allow you to power the motor board and control the motors using the Raspberry Pi.

### What you will need

+ Raspberry Pi
+ Motor controller board (wired up to the DC motors)
+ AA battery holder for four AA batteries
+ Four AA batteries
+ Five jumper leads (female-to-female)
+ Screwdriver

You may also need:

+ GPIO reference card

![Picture of the robot buggy parts for this step - Raspberry Pi, Motor controller board (wired up to the DC motors), AA battery holder (for 4 AA batteries), 4 x AA batteries, 5 x jumper leads (female-to-female), Screwdriver, GPIO reference card](images/1_6-parts-for-motor-board-raspberry-pi-and-battery-pack)

### Connect the battery pack to the motor board

The motors require more power than the Raspberry Pi can provide. Therefore, you will use four AA batteries to power them.

The battery pack should include two wires: one red and one black. The red wire is for the positive terminal and needs to be inserted into the **VCC** terminal block if it is present, or the 'voltage in' terminal block labelled **+12V** otherwise.

![Picture of the red wire from the battery pack connected to the 12V terminal block of the motor controller](images/1_6-battery-pack-red-wire-motor-controller)

The black wire is the ground wire and must be inserted into the **GND** terminal to complete the circuit. Make sure all the screws of the terminal blocks are tightened securely.

![Picture of the black wire from the battery pack connected to the GND terminal block of the motor controller](images/1_6-battery-pack-black-wire-motor-controller)

Insert the four AA batteries into the battery pack and if it has a switch, turn it on. Most motor controllers have a red LED that lights up to show that it is powered on. If the LED is not lit up, the wires may not be connected properly. Also check that your battery pack is full, and the batteries are the right way around.

### Receiving input

These instructions are for a L298N dual H-bridge DC stepper motor driver controller board, and they will be similar for most motor controller boards. Other boards may connect differently to the one that I'm using, and some boards can simply be placed onto the Raspberry Pi GPIO pins as a HAT. Check the documentation for your board if you are using a different one.

On this motor controller board there are pins labelled **IN1**, **IN2**, **IN3**, and **IN4**. Some motor boards also have one or two **GND** (ground) pins next to the **IN** pins, but this board does not.

![A L298N motor controller board with four IN screw terminals for connecting to an electric motor. The four IN terminals are circled.](images/1_6-motor-controller-board-in-circled)

Which GPIO pins you use on your Pi is up to you; I have used **GPIO 7**, **8**, **9**, and **10**. However, if you use different GPIO pins, make sure you remember which ones, as you will need to refer to them in the code.

Use five female-to-female jumper leads to connect the Raspberry Pi GPIO pins to the pins on the motor controller board. Each DC motor will need to need to use two **IN** pins to connect to the Raspberry Pi, so that the motor can turn in both directions. You will also need one **GND** pin to complete the circuits; this can be the same pin for both motors.

| GPIO pin   | Connects to   | Board pin   |
|:----------:|:-------------:|:-----------:|
|7           |<–>            |IN1          |
|8           |<–>            |IN2          |
|9           |<–>            |IN3          |
|10          |<–>            |IN4          |
|GND         |<–>            |GND          |

If your motor board does not have a **GND** pin, use the terminal block that the battery pack also uses. Strip the end of the wire for the **GND** pin and secure it into the **GND** terminal block that your battery pack feeds into. There will now be two wires fed into the **GND** block: one from the battery pack and one from the Raspberry Pi.

![Picture of the four IN pins from the motor controller connected to four GPIO pins on the Raspberry Pi, as well as a GND pin connected from the Pi to the motor controller](images/1_6-motor-controller-connected-to-raspberry-pi)

### Powering the Pi

The Raspberry Pi will need its own source of power. For testing, the Raspberry Pi can be plugged directly into the mains power supply. However, when you come to building the body of the buggy and making it move, the Raspberry Pi will need a mobile source of power. A USB powerbank is a good choice, as it will be fairly light for the chassis to carry, just make sure it is capable of powering the model of Raspberry Pi that you are using.

### Setting up your Raspberry Pi

If you are not familiar with setting up a Raspberry Pi and using it, follow this guide to [Getting started with Raspberry Pi](https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started).

The programming language I will be using in this course is **Python** together with a library called [GPIO Zero](https://gpiozero.readthedocs.io/en/stable/index.html), which provides an accessible way to control components through the GPIO pins.

Python and GPIO Zero will be installed by default if your Raspberry Pi is running the **Raspbian** operating system. Follow this guide to [Installing GPIO Zero](https://gpiozero.readthedocs.io/en/stable/installing.html) if you are using **Raspbian Lite** or another operating system.

If you would like to control your Raspberry Pi remotely from another computer, check out our guide to [Creating a virtual desktop using VNC Server](https://www.raspberrypi.org/documentation/remote-access/vnc/).

### Discussion

Did you have any problems connecting the motor board to the Raspberry Pi or to the battery pack?

What type of power supply are you using for your Raspberry Pi?

Leave your answers in the comments section below. 
