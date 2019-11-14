[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Connecting a motor to the motor board

In this step you will start by connecting the motors and then the battery holder to the motor controller board. Lastly, you will connect the motor board to the Raspberry Pi.

### What you will need

For this step you will need the following items:

+ DC motors (2 x minimum)
+ Motor controller board
<!-- + Raspberry Pi -->
+ AA battery holder (for 4 x AA batteries)
+ 4 x AA batteries
+ Jumper leads (male-male, female-male)
+ Screwdriver

You may also need:

+ Soldering iron
+ Solder
+ Tape
+ Wire strippers

**Using a soldering iron can be a bit daunting at first but whether you are new to soldering or a veteran solderer, [this tutorial](https://projects.raspberrypi.org/en/projects/getting-started-with-soldering) will provide you with some quick tips and tricks.**

![Picture of parts](images/)

### The DC motors

Most DC motors do not come with wires attached to them, which means you will need to attach your own using solder.

#### Preparing the wires

You will need 2 wires for each DC motor to connect it to the motor controller board. Alternatively, you can strip 2 jumper leads to expose the bare wire for attaching to each of the motors.

![Picture of partially stripped male-male jumper lead](images/)

Remove the soft plastic clip from the motors so the wires can be attached. You can use the flat head of a screwdriver to help remove the clip.

![GIF of the plastic clip from a DC motor being removed with the help of a flat head screwdriver](images/)

Thread the bare wire through the contact on the motor. Top tip: it may be easier to solder the wire to the contact on the motor if you bend the wire once it has passed through the contact.

![Picture of the wire bent through the contact on the motor](images/)

#### Soldering the wires

Heat up the soldering iron. Clean the soldering iron ~head~ before using it. You can use a damp sponge or damp cloth to remove any residue whilst the iron is hot.

Heat the contact for a second or two before applying the solder and ensure the solder has made enough contact between the wire and the contact.
Try not to touch the plastic coating / insulation of the wires or any plastic between the two contacts with the soldering iron or it will start to smoke.

Wait for a minute or two for the solder to cool and then gently try to move the wire to test if it is securely attached to the contact. If the wire does move, you can either reheat the applied solder with the soldering iron and realign the wire, or apply more solder to the connection.

Ensure the wires connected to the motor are secure and trimmed. Accidental touching of the metal casing can ~short the circuit and stop the motor from receiving consistent power~.

Reattach the plastic clips to the motors. It's also a good idea to wrap the ends of the motors in tape, to protect them and help keep the solder in good condition.

### Connect the motors to the motor controller board

<!-- Check correctness. Move to the end or next step. -->
A motor controller board will have pins or screw terminals for connecting a motor to it. A DC motor needs two pins or terminals for it to work, and a servo motor needs four pins or terminals.

![A motor controller board with four out screw terminals for connecting to an electric motor.](images/1_5-motor-controller-board.jpg)

Using a screwdriver, loosen the screws in the terminal blocks labelled **OUT1**, **OUT2**, **OUT3**, and **OUT4**. Have a look at the documentation for your board if your labels are different.

Strip the ends of the wires (you can snip off the male or female ends if you need to). Insert the stripped ends of one motor into the **OUT1** and **OUT2** terminals and the stripped ends of the second motor into the **OUT3** and **OUT4** terminals. Tighten the screws so the wires are secured firmly in the terminal blocks.

![A close up image of one or two motors connected to the OUT terminal blocks of a motor board with the screws of the terminal blocks tightened. The OUT labels are clearly visible.](images/)

### Connect the power supply to the motor board

The motors require more power than the Raspberry Pi can provide. Therefore, you will use four AA batteries to power them.

The battery pack should include 2 wires, one red and one black. The red wire is the power input and needs to be inserted into the **VCC** terminal block. Some motor boards do not have a **VCC** block so instead use the voltage in block labelled **+12V**.
<!-- +12V not +5V? -->

The black wire is to ground the power supply and must be inserted into the **GND** terminal. Make sure all the screws of the terminal blocks are tightened securely.

Insert the four AA batteries into the battery pack. If the battery pack is connected correctly, a red LED on the motor board should turn on.

### Discussion

+ Did you have any issues connecting the motors to the motor board?
+ Do you need help with anything that isn't working properly?

Share your thoughts with your fellow learners below.
