[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Connecting the Raspberry Pi to the motor board

Now you have attached the motors to the motor controller board, your next step is to connect the motor board to the GPIO pins on the Raspberry Pi. This will allow you to control the motors using the Raspberry Pi.

The board used in this project needs to be wired to the Raspberry Pi. Other boards may connect differently, and some boards can simply be placed onto the Raspberry Pi GPIO pins as a HAT. Make sure you look at the documentation for your board to see whether this is the case.

### What you will need

For this step you will need the following items:

+ Motor controller board
+ Raspberry Pi
+ Jumper leads (female-female)
+ Screwdriver

You may also need:

+ GPIO reference card

### Receiving input

On the board used here there are pins labeled **IN1**, **IN2**, **IN3**, and **IN4**, as well as two **GND** (ground) pins. Which GPIO pins on your Pi that you use is up to you; in this part of the project, **GPIO 7**, **8**, **9**, and **10** have been used.

Use five female-to-female jumper leads to connect the Raspberry Pi GPIO pins to the pins on the motor controller board. Each of your DC motors will need to need to use two **IN** pins to connect to the Raspberry Pi, as well as one **GND** pin.

| GPIO pin   | connects to   | board pin   |
|:----------:|:-------------:|:-----------:|
|7           |<–>            |IN1          |
|8           |<–>            |IN2          |
|9           |<–>            |IN3          |
|10          |<–>            |IN4          |
|GND         |<–>            |GND          |

If your board does not have a **GND** pin, then strip the end of the female-to-female or female-to-male wire and secure it into the **GND** terminal block that your battery pack feeds into. There will now be two wires fed into the **GND** block: one from the battery pack and one from the Raspberry Pi.

![The four In pins from the motor controller board connected to four GPIO pins on the Raspberry Pi as well as the GND pins connected from the board to the Pi.](images/)

### Powering the Pi

The Raspberry Pi will need its own source of power. A small USB power bank is the easiest way to power the Raspberry Pi. You could also make your own power bank though that is beyond the scope of this course. 

For testing purposes, the Raspberry Pi can be plugged directly into the mains power supply. However, when you come to building the body of the buggy and making it move then the Pi will need a mobile source of power. 

### Discussion

+ Did you have any problems connecting the motor board to the Raspberry Pi?
+ What type of power supple are you using for the Raspberry Pi?

Share your comments below.