[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Robotic Sensors

<INTRO PARAGRAPH>

### Force and Touch

When navigating the real world and interacting with physical objects, Robots can benefit from being able to sense the forces it is applying to these objects and forces exerted upon the Robot itself. 

**Force** 

Force sensors can be used by roboticists to detect the forces their robots are exerting on the objects they interact with. You heard of an example last week, where a robotic arm uses a pressure sensor to detect the force it is exerting on the mobile phone parts it picks up. It is important that the arm applies enough force to hold the part and not drop it, but not so much pressure that the component is damaged or crushed.

Other roboticists may use force sensors to detect external forces being applied to the robot. Force sensors can be used to detect shocks or vibrations that could allow a robot navigating dangerous terrain to react and balance/stabilise itself.

**Touch**

Touch sensors detect forces applied to a robot by a human. There are a few types of touch sensors that are commonly used. *Capacitive touch* sensors utilise the human body's conductive properties. The simplest form of a capacitor is made by holding 2 conductive materials close to each other, between them a small charge is stored. Capacitive touch sensors use the human finger as one of these plates and a plate behind the screen as the other. When the pad is touched the capacitance increases and the robot can sense this change. 

*Resistive touch* sensors do not use electrical properties, but instead they detect the pressure exerted by the touch. Once again 2 plates are used, when a user touches the top plate it touches a plate below it and a touch is registered. 

### Detecting the environment

Robots can use measurements of the environment around them to accomplish a variety of tasks, they are especially useful in environments that are hostile to humans (such as the rovers NASA and other space agencies send to explore Mars). There are plenty of uses for these sensors on earth as well, and you may want to include some of them on your buggy. 

**Temperature** 

Temperature sensors can be used in a variety of contexts, not just data collection for scientific experiments. A rover on Mars can use its temperature sensor to evaluate the terrain it is rolling over, if it detects a drop in temperature it can reduce the torque on it's wheels to prepare for ice. A robot designed to fight fires could use a temperature sensor to direct itself to the hottest parts of a burning building, where it will be most effective. Under water robots can use temperature sensor to follow under water currents and study the wildlife that thrives in warmer water. 

**Light** 

Another detectable property of the environment is light, which can also be used to accomplish a variety of tasks. One of the more obvious uses is for robots who have different tasks to accomplish at night than in the day, a robot can detect changes in light and change it's behaviour into night mode. Changes in light can also indicate a change in surroundings, a robot designed to explore houses in disaster zones could use it to navigate around a home that has collapsed. Directing itself towards the light to get out of tight spaces. 

**Sound** 

A sound sensor will measure the noise present in the robots environment, most will detect the presence of sound and also measure the amplitude of the sound. The higher the amplitude, the louder the noise. This could be used by a robot designed to study wildlife, by following noises and sounds where they are more intense. A more complex use could a sound sensor for speech recognition, responding to commands from a roboticist. 

**Chemical** 

Certain chemical properties can be measured by a robot using sensors. *pH* sensors detect the acidity/alkalinity of the environment around a robot. There are lots of uses for pH sensors in scientific robots, which use this detection in experiments (maybe in space). Carbon Monoxide sensors are another type of chemical sensor, which can be used to explore hostile environments where human explorers would be put at risk. 

### Object proximity

Mobile robots have to navigate the world around them, often autonomously, and there are sensors that help them detect the proximity of other objects around them. 

**Infrared Sensors** 

One method of detecting objects around a robot, is the use of infrared sensor. Infrared sensors detect changes in the levels of environmental infrared radiation, which is given off by objects that are hot (particularly living things). Infrared sensors are often used to detect motion, so they are particularly useful for robots that interact directly with humans. They are not very effective at detecting inanimate objects. 

**Ultrasonic Distance Sensors** 

A better sensor for robots that have to navigate around inanimate objects, is the UDS (ultrasonic distance sensor). These sensors emit high frequency noises, which rebound off of objects in the surrounding area and return to the robot. The gap between the emission and the return of the sound can be used to calculate the distance between the robot and the object that the sound bounced off of. 

I am going to show you how to use a UDS in your buggy, and in the next step you will see how they work in greater detail. 

### Sense your way. 

**Pick one of the types of sensor you have seen in this step.**

**Think of another use of that sensor in robotics, from past experience or your imagination** 

Share your ideas in the comments section. 