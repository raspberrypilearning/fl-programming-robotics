Welcome to *Robotics With Raspberry Pi: Build and Program Your First Robot Buggy*.

Over this course you'll develop a robot buggy and program it. You'll start by making it move about, before programming it to react to sensor readings. By the end of the course you'll be able to make your buggy avoid obstacles and follow a line on the floor.

### What you will learn

Over the next three weeks you will learn about:

+ Using the GPIO pins on the Raspberry Pi for both input and output
+ How to connect motors via a motorboard and control them using Python
+ Attaching components to a chassis
+ Using an ultrasonic distance sensor (UDS) to detect objects
+ Using inputs to control the outputs of your robot
+ How line sensors work
+ Using line sensors with your robot to detect and follow a line 
+ How changing an algorithm can improve the performance of your robot

### What you will need

This course requires you to have the following:

#### Hardware

+ Raspberry Pi 3B, 3B+, or 4
+ Motor controller board
+ Two 3V–6V DC motors
+ Two wheels
+ Ball caster (unless using more than two wheels)
+ An Ultrasonic Distance Sensor (UDS)
+ Two resistors for splitting the voltage if the UDS is 5V (e.g. a 1200 and a 2200 Ohm resistor)
+ Two line-following sensors
+ Jumper leads (female-to-female and male-to-female) or wire
+ AA battery holder (for four AA batteries)
+ Four AA batteries
+ A USB powerbank (to power the Raspberry Pi) 
+ Soldering iron and solder
+ Wire strippers
+ Scissors
+ Screwdriver
+ A small cardboard box for the chassis (can be plastic, wood, metal, etc.)
+ Black tape and white paper or card (to make a track with a black line for the line-following robot)

The hardware components and tools are listed in [this document](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/PDFs/Robot+buggy+components+and+tools+list.pdf). This list includes suggested models, types and pictures of each component, although alternatives are also available. You can also view most of the required components on this [AliExpress Wish List](https://my.aliexpress.com/wishlist/shared.htm?groupId=100000018016415), but they can be ordered and bought from many other suppliers.

#### Software

+ The latest version of the Raspbian operating system
+ An IDE of your choice

#### Additional extras

+ Adhesives (duct tape/electrical tape, putty, glue, etc.)
+ Cable ties or Velcro-type straps
+ GPIO reference card

Using a soldering iron can be a bit daunting at first, but whether you are new to soldering or a veteran, this [Getting started with soldering](https://projects.raspberrypi.org/en/projects/getting-started-with-soldering) resource will give you  some quick tips and tricks.

A Raspberry Pi model 3B or above is recommended, as you can connect to it over WiFi or Bluetooth without an adapter; this will help when programming the robot buggy.

The Ultrasonic Distance Sensor (UDS) and line-following sensors are required for weeks two and three respectively. 

If the UDS is 5V, you will need two resistors to split the voltage so that it can operate safely with the Raspberry Pi at 3.3V e.g. by using a 1200 and a 2200 Ohm resistor. Full instructions on how to do this are in week two of the course.

A ball caster is necessary if your robot has only two wheels; it will act as a third wheel so that the robot is balanced and can move freely.

### Choosing a programming environment

I recommend using an Integrated Development Environment (IDE) during this course to create, run, and test your Python programs.

The IDE I will be using is Mu, which is pre-installed on most Raspberry Pis. Mu is also available at the website [Code with Mu](https://codewith.mu/) along with [instructions on how to install Mu on a Raspberry Pi](https://codewith.mu/en/howto/1.0/install_raspberry_pi).

If you experience problems or would just like to know more about Mu, have a look at Raspberry Pi’s [Getting started with Mu](https://projects.raspberrypi.org/en/projects/getting-started-with-mu) guide.

### Week one

In week one of the course you will attach the motors and get your robot buggy moving.

What part of the course are you most looking forward to? Share your thoughts in the comments.

**Important note for teachers in England**: In order to get free upgraded access to this course, and to use it towards your National Centre for Computing Education certification, you must have joined the course through a link from the [Teach Computing](https://teachcomputing.org/courses) website. If you have not, [please join the course on this page](https://teachcomputing.org/courses/CO224/robotics-with-raspberry-pi-build-and-program-your-first-robot-buggy) and accept the invite on the next page. Failure to do this will mean that you will lose access to the course and it will not be counted towards the certification. Your eligibility for bursary payments may also be affected.

### Teach Computing Curriculum

Support and materials for teaching the topics covered in this course can be found in the [**Year 9 Physical Computing**](https://teachcomputing.org/curriculum/key-stage-3/physical-computing?utm_source=FutureLearn&utm_medium=LearningPlatform&utm_campaign=TCC_link&utm_content=robot) unit of the [Teach Computing Curriculum](https://teachcomputing.org/curriculum?utm_source=FutureLearn&utm_medium=LearningPlatform&utm_campaign=TCC_link&utm_content=robot).

The Teach Computing Curriculum contains lesson plans, slides, worksheets, homework and assessment activities to teach computing to children aged between 5 and 16

All of the content is completely free to access, and has been created by subject experts, based on the latest pedagogical research and teacher feedback. It provides an innovative progression framework where computing content (concepts, knowledge, skills, and objectives) have been organised into interconnected networks called learning graphs.

### Using the course content

The contents of this course are free for you to reuse. Unless otherwise specified, you can copy, and adapt the text, images and videos to use in your classes under the [Open Government Licence v3.0.](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/), so long as you attribute the Raspberry Pi Foundation as follows: **This text/image/video was created by the Raspberry Pi Foundation and is licensed under the [Open Government Licence v3.0](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)**.
