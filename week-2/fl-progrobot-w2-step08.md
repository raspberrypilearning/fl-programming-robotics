[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Programming the UDS

In the last step, you connected the ultrasonic distance sensor (UDS) to the Raspberry Pi and secured the UDS to the buggy. Now you will test that the UDS can detect objects at different distances directly in front of it.

### Testing the UDS

You need to make sure the UDS is working correctly whilst the buggy is not moving. To do this, you will be using the GPIO Zero library again.

**1.** Start by creating a new Python 3 file.

**2.** Next, you need to import the libraries for testing the UDS. GPIO Zero doesn't have a class specifically for a UDS, but instead you can use InputDevice and OutputDevice:

~~~ python
from gpiozero import InputDevice, OutputDevice
from time import sleep, time
~~~

You will need to use `time` and `sleep` to calculate the time taken for an echo to return after it has been triggered.

**2.** After the libraries have been imported, you can set up the trigger and echo pins of the distance sensor:

~~~ python
trig = OutputDevice(4)
echo = InputDevice(17)

sleep(2)
~~~

Remember that in the last step I chose to connect the `trig` pin on the UDS to GPIO pin 4 on the Raspberry Pi and the `echo` pin was connected to GPIO pin 17. You may have chosen different GPIO pins to me so make sure you check what they are for your setup and alter the code if the pins are different.

The `sleep(2)` is there to let the sensor settle itself when the program starts so that the readings are accurate.

**3.** You can create a function to send and receive a pulse next. The first thing to do is set the trigger pin to send out a burst of ultrasound for 10μs:

~~~ python
def get_pulse_time():
   trig.on()
   sleep(0.00001)
   trig.off()
~~~

**4.** As soon as the ultrasonic sensor has sent out a burst of sound from the `trig` pin, the `echo` pin is set to high. You can use a while loop inside the function to detect when this happens and then record the current time:

~~~ python
    while echo.is_active == False:
        pulse_start = time()
~~~

In the code above, the start time will continue to be replaced by the current time until the `echo` pin has been activated and set to high.

**5.** When an echo is received by the UDS, the echo pin is set to low. Another while loop inside the function will be able to record the time at which it happens:

~~~ python
    while echo.is_active == True:
        pulse_end = time()
~~~

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
