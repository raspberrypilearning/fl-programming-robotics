[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Robotic Sensors

Robots, particularly autonomous ones, need to sense the world around them. In this step I will take you through a few of the many options available to add sensing to your buggy.

### Force and Touch

A robot designed to navigate the real world and interact with physical objects - by picking them up for example - must be able to measure the force it is applying to these objects. In some cases it might be necessary for the bot to sense external forces exerted upon itself.

**Force**

Force sensors are used by roboticists to measure the forces their robots are exerting on the objects they interact with - like the robotic arm assembling mobile phones that you heard about last week. It is important that the arm applies enough force to hold the part and not drop it, but not so much pressure that the component is damaged or crushed.

Other roboticists use force sensors to detect shocks or vibrations, to allow a robot to react and balance/stabilise itself. Mobile robots could use force sensors in navigation as well - although touch sensors are more common.

**Touch**

Touch sensors allow robots to detect physical interactions between their body and objects in their surroundings. *Capacitive touch* sensors utilise conductive properties to detect touches, most commonly from a human's touch but any object that can conduct electricity will work. *Resistive touch* sensors do not use electrical properties, but instead they detect touches based on pressure applied to the plate. This type of sensor can allow a robot to navigate its surroundings, even if the object touching the sensor would not conduct electricity.

### Detecting the environment

Robots can use measurements of the environment around them to influence their behaviour, or just to collect data for analysis.

**Temperature**

Temperature sensors can be used in a variety of contexts, not just as data collection for scientific experiments. A rover on Mars can use its temperature sensor to evaluate the terrain it is rolling over; if it detects a drop in temperature it can reduce the torque on its wheels to prepare for ice. A robot designed to fight fires could use a temperature sensor to direct itself to the hottest parts of a burning building, where it will be most effective.

**Light**

Another detectable property of the environment is light. If a robot has different tasks to accomplish at night than in the day, it could detect decreasing light levels and change its behaviour to night mode. Changes in light can also indicate a change in surroundings; a robot designed to explore houses in disaster zones could use light sensors to help navigate around a home that has collapsed, by directing itself towards the light to get out of tight spaces.

**Sound**

Sound sensors act similarly to microphones but are often attached to circuits that compare the amplitude of the sound to a threshold value - returning the result of that comparison to the robot. The higher the amplitude, the louder the noise. This could be used by a robot designed to study wildlife, detecting and following loud noises may be one of the pieces of a data used to locate wildlife. A more complex use could a sound sensor for speech recognition, responding to commands spoken by a user.

**Chemical**

Robots can also use specialised sensors to detect certain chemical properties. *pH* sensors detect the acidity/alkalinity of the environment around a robot. Scientific robots could use this to check the quality of rivers or soil in remote places. Carbon monoxide is poisonous, robots equipped to sense the gas can be used to monitor potentially dangerous environments where human explorers may be put at risk.

### Object proximity

Mobile robots have to navigate the world around them, often autonomously, and there are sensors that help them detect the proximity of other objects around them.

**Infrared Sensors**

Infrared sensors detect changes in the levels of infrared radiation captured by the device. These changes are caused when an object (often a living thing) hotter than the background passes through the sensor's field of view.

**Ultrasonic Distance Sensors**

A better sensor for robots that have to navigate around inanimate objects is the UDS (ultrasonic distance sensor). These sensors emit high frequency noises, which rebound off of objects in the surrounding area and return to the robot. This is how bats sense the world when flying at night.

You are going to use a UDS in your buggy, and in the next step you will see how they work in greater detail.

### Sense your way.

**Pick one of the types of sensor you have seen in this step.**

**Think of another use of that sensor in robotics, from past experience or your imagination**

Share your ideas in the comments section.
