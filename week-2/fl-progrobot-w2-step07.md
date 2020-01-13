[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Attaching the UDS to the buggy

Having read about how a Ultrasonic Distance Sensor (UDS) works, you are now going to connect one to the Raspberry Pi.

If the UDS `echo` pin is 5V, for example for the HC-SR04 sensor, a voltage divider (as described earlier this week) is required to ensure the Pi is not damaged. Alternatively, a 3V3 tolerant  sensor (such as the HC-SR04P) will work without a voltage divider.

### What you will need

For this step, you will need the following items:

+ Ultrasonic distance sensor <!-- Check aliexpress wishlist -->
+ 4 x female-male jumper leads

If your UDS is 5V, you will also need:

+ Soldering iron and solder
+ 330 Ohm resistor <!-- Change to: 2 different sized resistors to split the voltage e.g. a 330 Ohm resistor and a 470 Ohm resistor -->
+ 470 Ohm resistor
+ 2 more female-male jumper leads (6 in total)
+ Tape

![Picture of the robot buggy parts for this step - Ultrasonic distance sensor, 6 x female-male jumper leads, Soldering iron and solder, 330 Ohm resistor, 470 Ohm resistor, Tape](images/2_7-parts-for-the-UDS)

### Wiring the UDS

It is best to set up the UDS with the Raspberry Pi switched off, especially if your UDS is 5V. Otherwise, if make a mistake with your wiring and the Raspberry Pi is turned on, you might damage either it or the UDS.

Be aware that the instructions for wiring the UDS to the Raspberry Pi are slightly different depending on whether your UDS is 3.3V or 5V. Diagrams of both completed setups are shown below.

As discussed previously, a typical UDS has 4 pins: `VCC`, `Trig`, `Echo` and `GND`. All of these pins need to be connected to the Raspberry Pi.

**1.** Start by connecting a 5V pin on the Raspberry Pi into the `VCC` pin on the UDS using a female-male jumper lead. Refer to the diagram below or a GPIO reference guide if you aren't sure which pin on the Pi to use.

![The layout of the GPIO pins on a 40 pin Raspberry Pi using GPIO numbering, which can be used as a reference guide](images/1_4-gpio-numbers-raspberry-pi-40-pin-header.png)

**2.** The `Trig` pin on the UDS can connect straight into `GPIO 4` in the Raspberry Pi. You can use a different GPIO pin on the Raspberry Pi, although if you do the diagram below won't match your setup completely.

**3.** The `GND` from the UDS can go into any ground pin on the Raspberry Pi.

**4.** The wiring of the `Echo` pin depends on whether the UDS is 3.3V or 5V.

#### Wiring the `Echo` pin on a 3.3V UDS

Wiring a **3.3V** UDS is fairly simple as the output voltage of the `Echo` pin does not need to be reduced. The `Echo` pin on the UDS can connect straight into `GPIO 17` on the Raspberry Pi.

The diagram below shows you the complete setup for a **3.3V** UDS:

![Remove the vibration sensor and two connections (GP14 and GND) from the illustration. Replace the green, orange and black wires with one connection from Echo straight to GP17 and remove the two resistors](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/See_Like_A_Bat_Diagram_7.png)

#### Wiring the `Echo` pin on a 5V UDS

If the output of the `Echo` pin is **5V**, which will damage your Raspberry Pi, you need to reduce the output voltage to a **maximum of 3.3V**.

The resistors I use in this example are 330 Ohm and 470 Ohm, as this will give me an output of roughly ____ V. I can check this using the voltage divider algorithm used previously. You can use different resistors to the ones I chose but you must ensure that the voltage across the larger resistor has been reduced to 3.3V or just below.

The first thing to do is to solder the pair of resistors together, and then add female jumper leads to each end of the pair. This is usually easier with two people - one to hold the parts together and the other to solder - just be careful with the hot soldering iron and everyone's fingers!

Once the solder is cooled, add tape or heat-shrink to secure and insulate the joins:

![Image of two resistors soldered together with one female jumper lead soldered to the other end of each resistor - taken from project "See like a bat"](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/joined_resistors.jpg)

Next, add a third female jumper lead to the join between the two resistors. This can then be taped up as well:

![Image of the third female jumper lead soldered to the join between the two resistors - also taken from the project site](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/t_join.jpg)

Now you need to attach the jumper leads to the UDS and the Raspberry Pi.

+ The lead that joins to the **smaller** of the two resistors needs to go into the `Echo` pin on the UDS.
+ The lead that branches out from **between** the resistors should go into `GPIO 17`
+ The lead that comes out of the **larger** of the two resistors must go into a ground pin on the Raspberry Pi.

The diagram below shows you the complete setup for a **5V** UDS:

![Remove the vibration sensor and two connections (GP14 and GND) from the image](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/See_Like_A_Bat_Diagram_7.png)

### Securing the UDS to the buggy

Now that the UDS is connected to the Raspberry Pi you will need to attach the UDS to the robot buggy. The UDS will be detecting objects whilst the buggy is moving forwards, therefore you will need to secure the UDS to the front of the buggy.

Using a pencil, mark where you want the emitters and receivers (the two silver cylinders from the diagram above) to protrude from the buggy.

![Picture of the UDS cylinders being marked on the chassis were they need to be secured](images/2_7-marking-UDS-on-the-chassis)

Cut a hole into the buggy container that is just big enough for the emitters and receivers to poke through. You can also use tape to secure the UDS more securely to the chassis.

![Picture of the UDS attached to the chassis](images/2_7-UDS-attached-to-chassis)

### Checking the connections

Double check all your pins are connected properly before turning on the Raspberry Pi. It's easy for the jumper leads to come loose from the Raspberry Pi whilst you are moving parts of the robot buggy around.

Share any issues you had with wiring the UDS or attaching it to the buggy in the comments.