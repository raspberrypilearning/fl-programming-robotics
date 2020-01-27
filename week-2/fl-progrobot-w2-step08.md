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

#### Setting up the program

**1.** In a new Python 3 file, import the libraries required for this program.

~~~ python
from gpiozero import InputDevice, OutputDevice
from time import sleep, time
~~~

`InputDevice` and `OutputDevice` will be used to communicate with the **Trig** and **Echo** pins. You will also need `time` and `sleep` to calculate the time taken for the ultrasound to be emitted and received. 

**2.** Set up the **Trig** and **Echo** pins using the GPIO pins you connected them to on your Pi. 

~~~ python
trig = OutputDevice(4)
echo = InputDevice(17)

sleep(2)
~~~

I connected the **Trig** pin to **GPIO 4** and the **Echo** pin to **GPIO 17** but yours might be different.

The `sleep(2)` is there to let the sensor settle itself when the program starts so that the readings are accurate.

#### Transmitting and receiving the ultrasound

**3.** Create a function that will be used to calculate how long it takes for the ultrasound to be transmitted and received. 

~~~ python
def get_pulse_time():
   trig.on()
   sleep(0.00001)
   trig.off()
~~~

The function starts by setting the **Trig** pin to high for 10μs (microseconds) which prepares the internal clock of the UDS. 

As soon as the Trig pin is set to low, a burst of ultrasound is sent from the emitter and the sound starts to travel through the air.

![Animation of the Trig pin being set to high for 10μs and then Trig is set low. A burst of ultrasound is emitted from the UDS as soon as the Trig pin is set to low.](https://howtomechatronics.com/wp-content/uploads/2015/07/Ultrasonic-Sensor-Diagram.png)

Once the ultrasound has finished being transmitted, the Echo pin is set to high. At this point, you need to record the start time. 

**4.** Use a `while` loop inside the function to continuosly replace the start time until all of the sound has been transmitted.

~~~ python
    while echo.is_active == False:
        pulse_start = time()
~~~

`is_active` will return `True` if the **Echo** pin is high and `False` if the **Echo** pin is low.

![Animation showing that once the ultrasound has finished being transmitted, the Echo pin is set to high and the start time is recorded.](https://howtomechatronics.com/wp-content/uploads/2015/07/Ultrasonic-Sensor-Diagram.png)

If the ultrasound hits an object, it is reflected back to the sensor. As soon as the receiver picks up the ultrasound, the Echo pin is set to low and the end time needs to be recorded. 

**5.** Create another `while` loop inside the function that keeps replacing the end time until the **Echo** pin is set to low.

~~~ python
    while echo.is_active == True:
        pulse_end = time()
~~~

![Animation showing that if the ultrasound hits an object, it is reflected back to the sensor. As soon as the receiver picks up the ultrasound, the Echo pin is set to low and the end time is recorded. ](https://howtomechatronics.com/wp-content/uploads/2015/07/Ultrasonic-Sensor-Diagram.png)

**6.** The final part of this function requires you to return the amount of time it took for the pulse of ultrasound to be sent and received.

~~~ python
    return pulse_end - pulse_start
~~~

So far, all of the code from steps **3-6** should be inside the function you created called `get_pulse_time()`.

**7.** You can test the program by running it and then typing the following into the Python shell (known as the REPL if you are using Mu).

~~~ python
print(get_pulse_time())
~~~

Try typing the above line of code when your hand is close to and far from the distance sensor. You should get smaller values as your hand approaches the sensor since the sound will have travelled less distance.

### Calculating the distance

You can use a formula to calculate the distance the sensor is from an object, starting with the speed equation:

![speed = distance / time](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/speed.png)

This can be rearranged to make:

![distance = speed * time](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/distance.png)

But as the sound has to travel to the object **and** back again, you need to divide the calculated distance by 2. Therefore:

![distance = speed * time / 2](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/distance2.png)

The speed of sound in air will vary depending on the temperature and air pressure, but it tends to hover around 343 metres per second.

#### Putting the formula into practice

**8.** Create another Python function to calculate the distance.

~~~ python
def calculate_distance(duration):
    speed = 343
    distance = speed * duration / 2 # calculate distance in metres
    return distance
~~~

Using a different function to perform a separate piece of functionality is good coding practice.

**9.** Add an infinite loop to the bottom of the program to test everything works. 

~~~ python
while True:
	duration = get_pulse_time()
	distance = calculate_distance(duration)

	sleep(0.06)
	print(distance)
~~~

You need to let the UDS wait for a little bit before it can be used again, hence the `sleep` command inside the loop.

### The final program

Your full code should now look similar to this:

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

	return pulse_end - pulse_start

def calculate_distance(duration):
	speed = 343
	distance = speed * duration / 2
	return distance

while True:
	duration = get_pulse_time()
	distance = calculate_distance(duration)

	sleep(0.06)
	print(distance)
~~~

**10.** Run your code and you should see a stream of numbers, showing you the distance from the sensor in metres. Move your hand (or even better, a large flat object such as a book) closer to and further from the distance sensor.

### Testing the distances

What are the range of values that your UDS is outputting?

What happens if you place an object really close or far away from the UDS?

Share your answers in the comments below.
