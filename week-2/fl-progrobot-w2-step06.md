[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Distance Sensors

In this step I am going to break down the Ultrasonic distance sensor mentioned previously. Your robot buggy will use one of these sensors to navigate the physical world around it. Before you wire and code this functionality for your buggy, you should first get to know how these sensors work.

### Ultrasound

Ultrasonic distance sensors (UDS) use ultrasound to measure distances. Sound travels through the air in a *wave pattern*, measurements are made by examining the properties of the pattern over space and time.

As the sound travels the particles are oscillating back and forth, this is hard to draw so it is represented as a wave moving up and down on a graph. A sounds frequency is the number of oscillations per second. Frequency is measured in Hertz (Hz), if a wave oscillates once a second it is said to have a frequency of 1Hz. 

![A few waves showing the difference between high and low frequency sounds.](images/frequency_example.png)

*Ultrasound* refers to any sound that has a frequency that is above the human range of hearing, this level changes from person to person but on average anything 20kHz or above is considered ultrasound. This means the sound wave oscillates 20000 times a second or more.

The uses of ultrasound are widespread; doctors use the sound waves to scan inside human bodies, robots can use it to navigate the world and [engineers use it to reinforce metals by compressing the particles]().

### Ultrasonic distance sensor

![Ultrasonic distance sensor - taken from projects site](https://projects-static.raspberrypi.org/projects/see-like-a-bat/fac1abdedade76d99cbc5231ddf6ec3da912eebc/en/images/Ultrasonic_Distance_Sensor.png)

An ultrasonic distance sensor (UDS) works by sending out a burst of ultrasound. This sound will travel through air, but reflect back (echo) off of surrounding objects. The sensor can detect the echo, when it returns.

Using a measure of the time between the outgoing burst and returning echo, and the speed of sound, you can calculate how far an object is away from the sensor.

Commonly, a UDS require 2 components to do this; an emitter and a receiver. You can see this in the picture above, the two silver cylinders on the front of the sensor are the emitter and receiver.

A particular advantage of these sensors over other distance measurers, specifically those that use light, is that UDS are not effected by the colour of the object that echoes it's signal. Although errors can occur if the object can reflect sound away from the receiver.

### How to use a UDS

Now that you have a better idea of what a UDS is and how they work, you can move on to a more practical examination of how to use one with your buggy.

UDSs typically have 4 pins;

+ **VCC** is the pin that powers the device. It needs 5V to work.
+ **Trig** is the pin that triggers the emission of the ultrasound burst. It can be triggered using 3.3V.
+ **Echo** is the pin that outputs when the reflected sound is received. It outputs at 3.3V or 5V depending on the UDS model.
+ **GND** is the ground pin, used to complete the circuit.

If the UDS is 5V tolerant, this causes some issues because the **Echo** pin will output 5V and the Pi can only handle 3.3V. This means you will have to use some resistors to create a voltage divider - also known as a potential divider.

#### Voltage dividers

A voltage (or potential) divider can split a voltage into two smaller voltages. It does this by using resistors. Look at the diagram below. It shows a single resistor connected to a 5V pin. The voltage across the resistor is 5V:

![Potential divider images taken from projects site](https://projects-static.raspberrypi.org/projects/see-like-a-bat/fac1abdedade76d99cbc5231ddf6ec3da912eebc/en/images/See_Like_A_Bat_Diagram_2.png)

Now look at the diagram below. By using two resistors wired in series, the voltage can be split. As both resistors are the same, the voltage is split equally between the two:

![Same again](https://projects-static.raspberrypi.org/projects/see-like-a-bat/fac1abdedade76d99cbc5231ddf6ec3da912eebc/en/images/See_Like_A_Bat_Diagram_3.png)

By altering the resistors, we can tailor the voltage across any one of them to be anything we like. Here you can see that we have split the voltage to give us almost exactly 3.3V:

![And agaaain](https://projects-static.raspberrypi.org/projects/see-like-a-bat/fac1abdedade76d99cbc5231ddf6ec3da912eebc/en/images/See_Like_A_Bat_Diagram_4.png)

To work out the resistors you need, you can use the code below.

~~~python
R1 = 1200 # Your current resistor (alter this)
Vout = 3.3 # The voltage you are trying to achieve (always 3.3)
Vin = 5 # The input voltage (always 5)

R2 = (Vout * R1) / (Vin - Vout)

print('The resistor you need is approximately', R2)
~~~

### Limitations of a UDS

The biggest limitation of this type of sensor comes when the object that reflects the ultrasound is very close. In this case the receiver might not pick up the sound when it is initially reflected off an object, and instead detect the sound once it has rebounded off another object. This results in a higher distance reading than is accurate.

### Test your voltage divider

Using the code and formula above, what size resistors could you use to limit the voltage to 1V?

Share your thinking and answers in the comments below.
