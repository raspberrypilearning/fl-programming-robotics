[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Attaching the UDS to the buggy

Now that you have read about how a UDS works, you are going to connect one to your Raspberry Pi. Make sure to check whether you need a voltage divider: check the model number or post a photo in the comments if you are unsure.

### What you will need

For this step, you will need the following items:

+ Ultrasonic distance sensor
+ Four female-to-female jumper leads

If your UDS is 5V, you will also need:

+ Two different resistors to split the voltage (e.g. a 330-ohm resistor and a 620-ohm resistor)
+ Two more female-to-female (six in total)
+ Soldering iron and solder
+ Tape

![Picture of the robot buggy parts for this step - Ultrasonic distance sensor, 6 x female-to-female jumper leads, Soldering iron and solder, 330 Ohm resistor, 620 Ohm resistor, Tape](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/2_7-parts-for-the-UDS.jpg)

### Wiring the UDS

It is best to set up the UDS with the Raspberry Pi switched off, especially if your UDS is 5V. Otherwise, if you make a mistake with your wiring and the Raspberry Pi is turned on, you might damage it or the UDS.

As discussed previously, a typical UDS has four pins: **VCC**, **trig**, **echo**, and **GND**. All of these pins need to be connected to your Raspberry Pi.

The **trig** and **echo** pins can be wired to any available GPIO pins on your Pi, though if you choose different pins to the set-up below, the diagrams won't match. You'll also need to remember what pins you used and replace the pin numbers in the code accordingly.

Refer to the diagrams in this article or a GPIO reference guide if you aren't sure which pins on the Raspberry Pi to use.

![The layout of the GPIO pins on a 40-pin Raspberry Pi using GPIO numbering, which can be used as a reference guide](images/1_4-gpio-numbers-raspberry-pi-40-pin-header.png)

#### Wiring the VCC, trig, and GND pins

1. Start by connecting the **VCC** pin on your UDS to a 5V pin on your Raspberry Pi, using a female-to-female jumper lead.

2. Connect the **trig** pin on the UDS to an available GPIO pin on your Raspberry Pi; I've used **GPIO 4**.

3. Connect the **GND** pin from your UDS to a ground pin on your Raspberry Pi.

The instructions for wiring the **echo** pin are different depending on whether the UDS is **3.3V-tolerant** or **5V-tolerant**.

#### Wiring the echo pin on a 5V UDS

If the output of the echo pin is 5V, you need to reduce the output voltage to a **maximum of 3.3V**.

For the purposes of this example, I'm going to use a 330-ohm resistor and a 620-ohm resistor. You can use different resistors to these, but you must ensure that the voltage across the larger resistor has been reduced to 3.3V or just below, using the voltage divider algorithm seen previously.

The first thing to do is to solder the pair of resistors together. Then you need to solder a female jumper lead to the other end of each resistor. This part might be easier to do with two people or by using a [helping hand](https://www.instructables.com/id/How-to-Make-a-Helping-Hands-for-Soldering-at-Home-/). Once the solder has cooled, add tape to secure and insulate all of the joins.

![Picture of two resistors soldered together with one female jumper lead soldered to the other end of each resistor - taken from project "See like a bat"](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/2_7-resistors-and-jumper-leads-soldered-together.jpg)

Next, attach a third female jumper lead to the join between the two resistors. Add tape to secure this join in place.

![Picture of the third female jumper lead soldered to the join between the two resistors - also taken from the project site](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/2_7-third-jumper-lead-soldered-to-resistors.jpg)

Now you need to attach the jumper leads to your UDS and the Raspberry Pi.

+ The lead that joins to the **smaller** of the two resistors needs to go into the **echo** pin on your UDS
+ The lead that branches out from **between** the resistors should go into **GPIO 17**
+ The lead that comes out of the **larger** of the two resistors must go into a ground pin on your Raspberry Pi

The diagram below shows you the complete set-up for a 5V UDS:

![A UDS with wires and two resistors connecting to a Raspberry Pi GPIO reference board. The VCC wire on the UDS connects to 5V, Trig connects to GP4, and GND connects to GND on the reference card. The Echo pin on the UDS connects to a 330 ohm resistor, which connects to a 620 ohm resistor and a wire that connects to GP17 on the reference card. The 620 ohm resistor also connects to GND on the reference card](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Illustration/29-2_7-wiring-5V-UDS-diagram.png)

#### Wiring the echo pin on a 3.3V UDS

Wiring a 3.3V UDS is fairly simple, as the output voltage of the echo pin does not need to be reduced.

The diagram below shows you the complete set-up for a 3.3V UDS, with the echo pin connected to **GPIO 17** on the Raspberry Pi:

![A UDS with four wires connecting to a Raspberry Pi GPIO reference board. The VCC wire on the UDS connects to 5V, Trig connects to GP4, Echo connects to GP17, and GND connects to GND on the reference card.](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Illustration/28-2_7-wiring-3V3-UDS-diagram.png)

### Securing the UDS to the chassis

Now that your UDS is connected to your Raspberry Pi, you will need to attach the UDS to the front of the chassis so that your robot can detect objects in front of the buggy.  

Mark where you want the emitter and receiver (the two silver cylinders from the diagram above) to protrude from the chassis.

![Picture of the UDS cylinders being marked on the chassis were they need to be secured](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/2_7-marking-UDS-on-the-chassis.jpg)

Cut two holes into the chassis that are just big enough for the emitter and receiver to poke through, then push the cylinders through the holes. You can also add tape to attach the UDS more securely to the chassis.

![Picture of the UDS attached to the chassis](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Photographs/2_7-UDS-attached-to-chassis.jpg)

### Checking the connections

It's easy for the jumper leads to come loose from the Raspberry Pi while you are moving parts of the robot around, so double-check that all your pins are connected properly before turning on your Pi.

### Discussion

Share any issues you had with wiring the UDS or attaching it to the chassis in the comments.
