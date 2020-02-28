[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Programming the UDS

Now that you've attached the ultrasonic distance sensor (UDS), you need to test that it can detect objects that are directly in front of it at different distances.

### Testing the UDS

First, you need to check that the UDS is working correctly while the robot is stationary. To interact with the UDS, you will be using the GPIO Zero library.

#### Setting up the program

**1.** In a new Python 3 file, import the libraries required for this program.

~~~ python
from gpiozero import InputDevice, OutputDevice
from time import sleep, time
~~~

`InputDevice` and `OutputDevice` will be used to communicate with the trig and echo pins. You will also need `time` and `sleep` to calculate the time taken for the ultrasound to be emitted and received.

**2.** Set up the trig and echo pins using the GPIO pins you connected them to on your Raspberry Pi. I used pins 4 and 17 respectively, but you may have used different pins.

~~~ python
trig = OutputDevice(4)
echo = InputDevice(17)

sleep(2)
~~~

The `sleep(2)` is there to let the sensor settle when the program starts, so that the readings are accurate.

#### Transmitting and receiving the ultrasound

**3.** Create a function that will be used to calculate how long it takes for the ultrasound to be transmitted and received.

Start by setting the trig pin to high for 10μs (microseconds), which prepares the internal clock of the UDS.

~~~ python
def get_pulse_time():
   trig.on()
   sleep(0.00001)
   trig.off()
~~~

As soon as the trig pin is set to low, a burst of ultrasound is sent from the emitter, and this sound starts to travel through the air.

![Animation of the Trig pin being set to high for 10μs and then set to low. A burst of ultrasound is emitted from the UDS as soon as the Trig pin is set to low.](https://howtomechatronics.com/wp-content/uploads/2015/07/Ultrasonic-Sensor-Diagram.png)

Once the ultrasound has finished being emitted, the UDS sets the echo pin to high. At this point, you need to record the start time.

**4.** Use a `while` loop inside the function to record the start time.

~~~ python
    while echo.is_active == False:
        pulse_start = time()
~~~

You can use the `is_active` command to check if a pin is set to high (which returns `True`) or low (which returns `False`).

The above code works by repeatedly replacing the value of `pulse_start` with the current time until the echo pin is active. This means that the final value of `pulse_start` is the time at which the echo pin is set to high.

![Animation showing that once the ultrasound has finished being transmitted, the Echo pin is set to high and the start time is recorded.](https://howtomechatronics.com/wp-content/uploads/2015/07/Ultrasonic-Sensor-Diagram.png)

If the ultrasound hits an object, it is reflected back to the sensor. As soon as the receiver picks up the ultrasound, the echo pin is set to low and the program must record the end time.

**5.** Inside the function, create another `while` loop that keeps replacing the end time until the echo pin is set to low.

~~~ python
    while echo.is_active == True:
        pulse_end = time()
~~~

![Animation showing that if the ultrasound hits an object, it is reflected back to the sensor. As soon as the receiver picks up the ultrasound, the Echo pin is set to low and the end time is recorded. ](https://howtomechatronics.com/wp-content/uploads/2015/07/Ultrasonic-Sensor-Diagram.png)

**6.** Finally, the function should return the amount of time it took for the pulse of ultrasound to be sent and received.

~~~ python
    return pulse_end - pulse_start
~~~

All of the code from steps 3 to 6 should be inside the function you created called `get_pulse_time()`.

**7.** Test the program by running it and then typing the following into the Python shell (known as the REPL if you are using Mu).

~~~ python
print(get_pulse_time())
~~~

Try typing the above line of code when your hand is at different distances from the front of the UDS. You should get smaller values as your hand approaches the sensor.

### Calculating the distance

You can use a formula to calculate the distance the sensor is from an object, starting with the speed equation:

![speed = distance / time](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/speed.png)

This can be rearranged to make:

![distance = speed * time](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/distance.png)

but as the sound has to travel to the object **and** back, you need to divide this distance by 2:

![distance = speed * time / 2](https://projects-static.raspberrypi.org/projects/see-like-a-bat/88c95cc4c253c700132e4c26f23373c277241549/en/images/distance2.png)

The speed of sound in air will vary depending on the conditions, but it tends to hover at around 343 metres per second.

#### Putting the formula into practice

**8.** Create another function to calculate the distance.

~~~ python
def calculate_distance(duration):
    speed = 343
    distance = speed * duration / 2
    # calculate distance in metres
    return distance
~~~

Using a different function to calculate this distance is good coding practice, as this function can be tested separately, and can easily be reused multiple times within the program.

**9.** Add an infinite loop to the bottom of the program to test that everything works.

~~~ python
while True:
	duration = get_pulse_time()
	distance = calculate_distance(duration)

	sleep(0.06)
	print(distance)
~~~

You need the `sleep` command, as the UDS requires a short wait before it can be used again.

### The final program

Your full code should now look similar to [this finished program](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/code/uds-detect-objects.py).

**10**. Run your code and you should see a stream of numbers showing you the distance of an object from the sensor in metres. Test this by moving a large, flat object such as a book closer to and further from the distance sensor.

### Testing the distances

What range of values is your program outputting?

What happens if you place an object really close to, or far away from, the UDS?

Share your answers in the comments below.
