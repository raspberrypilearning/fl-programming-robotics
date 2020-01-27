[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Programming the UDS

In the last step, you connected your ultrasonic distance sensor (UDS) to your Raspberry Pi and secured the UDS to the chassis. Now you will test that the UDS can detect objects at different distances directly in front of it.

### Testing the UDS

Firstly, you need to make sure the UDS is working correctly whilst the robot is stationary. To interact with the UDS, you will be using the GPIO Zero library.

**1.** Start by creating a new Python 3 file.

**2.** Next you need to import `InputDevice` and `OutputDevice` from the GPIO Zero library, which you will use to communicate with the **Trig** and **Echo** pins. 

~~~ python
from gpiozero import InputDevice, OutputDevice
from time import sleep, time
~~~

You will also need to use `time` and `sleep` to calculate the time taken for the ultrasound to be transmitted and received. 

**3.** Set up the **Trig** and **Echo** pins of the distance sensor using the GPIO pins you connected to on your Raspberry Pi. In the last step, I connected the **Trig** pin to **GPIO 4** and the **Echo** pin to **GPIO 17** but yours might be different.


~~~ python
trig = OutputDevice(4)
echo = InputDevice(17)

sleep(2)
~~~

The `sleep(2)` is there to let the sensor settle itself when the program starts so that the readings are accurate.

**4.** Create a function that will be used to detect how long it takes for the ultrasound to be transmitted and received. 


You can create a function to send and receive a pulse next. The first thing to do is set the trigger pin to send out a burst of ultrasound for 10μs:

~~~ python
def get_pulse_time():
   trig.on()
   sleep(0.00001)
   trig.off()
~~~

The function firstly sets the Tigger pin to high for 10μs (10 microseconds) which prepares the internal clock of the UDS.

![Animation of the Trig pin being set to high for 10μs and then Trig is set low. A burst of ultrasound is emitted from the UDS as soon as the Trig pin is set to low.](https://howtomechatronics.com/wp-content/uploads/2015/07/Ultrasonic-Sensor-Diagram.png)

As soon as the Trigger pin is set to low, a burst of ultrasound is sent from the emitter and the sound starts to travel through the air. The Echo pin remains at low whilst the ultrasound is being emitted. 

Once the ultrasound has finished being transmitted, the Echo pin is set to high and the start time is recorded. 

**4.** You can use a `while` loop inside the function to detect when the ultrasound has stopped being transmitted and the Echo pin is set to high.

~~~ python
    while echo.is_active == False:
        pulse_start = time()
~~~

The `is_active` command returns `True` if the Echo pin is high and `False` if the Echo pin is low. In this loop, `pulse_start` will continue to be replaced with the current time until Echo is `True` and the ultrasound has stopped being emitted from the sensor.

![Animation showing that once the ultrasound has finished being transmitted, the Echo pin is set to high and the start time is recorded.](https://howtomechatronics.com/wp-content/uploads/2015/07/Ultrasonic-Sensor-Diagram.png)

If the ultrasound hits an object, it is reflected back to the sensor. As soon as the receiver picks up the ultrasound, the Echo pin is set to low and the end time needs to be recorded. 

**5.** Create another `while` loop inside the function that repeats until the Echo pin is set to low and the end time is recorded.

~~~ python
    while echo.is_active == True:
        pulse_end = time()
~~~

![Animation showing that if the ultrasound hits an object, it is reflected back to the sensor. As soon as the receiver picks up the ultrasound, the Echo pin is set to low and the end time is recorded. ](https://howtomechatronics.com/wp-content/uploads/2015/07/Ultrasonic-Sensor-Diagram.png)

**6.** Next, you need to let the UDS sleep for a little bit before it can be used again. Then you can return the length of time it took for the pulse to be sent and received:

~~~ python
    sleep(0.06)

    return pulse_end - pulse_start
~~~

So far, all of the code from steps **3-6** should be inside the function you created called `get_pulse_time()`.

**7.** To finish off, you can test the program by running it and then typing the following into the Python shell (known as the REPL if you are using Mu).

~~~ python
print(get_pulse_time())
~~~

Try typing the above line of code when your hand is close to and far from the distance sensor. You should get smaller values as your hand approaches the sensor since the sound will have travelled less distance.

### Calculating the distance

There’s a simple formula for calculating the distance the sensor is from an object. You can start off with the speed equation:

![speed = distance / time](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/speed.png)

This can be rearranged to make:

![distance = speed * time](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/distance.png)

But you need to remember that as the sound has to travel to the object and back again, we need to divide the calculated distance by 2. Therefore:

![distance = speed * time / 2](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/distance2.png)

The speed of sound in air will vary depending on the temperature and air pressure, but it tends to hover around 343 metres per second.

We can write a simple Python function to calculate the distance for us:

~~~ python
def calculate_distance(duration):
    speed = 343
    distance = speed * duration / 2 # calculate distance in metres
    return distance
~~~

To test everything is working, we can add an infinite loop at the bottom of the program. Your full code should now look like this:

~~~ python
from gpiozero import InputDevice, OutputDevice
from time import sleep, time

trig = OutputDevice(4)
echo = InputDevice(17)

sleep(2)

def get_pulse_time():
    trig.on()
   	sleep(0.00001)
	trig.off()

	while echo.is_active == False:
		pulse_start = time()

	while echo.is_active == True:
		pulse_end = time()

	sleep(0.06)

	return pulse_end - pulse_start

def calculate_distance(duration):
	speed = 343
	distance = speed * duration / 2
	return distance

while True:
	duration = get_pulse_time()
	distance = calculate_distance(duration)
	print(distance)
~~~

Run your code and you should see a stream of numbers, showing you the distance from the sensor in metres. Move your hand (or even better, a large flat object such as a book) closer to and further from the distance sensor.

### Testing the distances

What are the range of values that your UDS is outputting?

What happens if you place an object really close or far away from the UDS?

Share your answers in the comments below.
