[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Robotic Sensors

Robots, particularly autonomous ones, should be able to sense the world around them in some way. There are lots of different sensors you can use in your robotics projects. In this step I will take you through some of the options you can use to add sensing to your buggy.

### Force and Touch

When navigating the real world and interacting with physical objects, Robots can benefit from being able to sense the forces it is applying to these objects, and forces exerted upon the Robot itself.

**Force**

Force sensors can be used by roboticists to detect the forces their robots are exerting on the objects they interact with. You heard of an example last week, where a robotic arm uses a pressure sensor to detect the force it is exerting on the mobile phone parts it picks up. It is important that the arm applies enough force to hold the part and not drop it, but not so much pressure that the component is damaged or crushed.

Other roboticists may use force sensors to detect external forces being applied to the robot. Force sensors can be used to detect shocks or vibrations that could allow a robot to react and balance/stabilise itself.

**Touch**

Touch sensors can be used to detect forces applied to a specific point on a robot. *Capacitive touch* sensors utilise the human body's conductive properties to detect finger presses or other touches. They can also detect touches from any object that can conduct electricity. An example use might be to change the behaviour the robot is exhibiting when someone presses the touch pad. *Resistive touch* sensors do not use electrical properties, but instead they detect the pressure exerted by the touch. This type can be used to navigate a robots surroundings, as the object touching it does not have to conduct electricity.

### Detecting the environment

Robots can use measurements of the environment around them to accomplish a variety of tasks. They are especially useful in environments that are hostile to humans (such as the rovers NASA and other space agencies send to explore Mars).

**Temperature**

Temperature sensors can be used in a variety of contexts, not just data collection for scientific experiments. A rover on Mars can use its temperature sensor to evaluate the terrain it is rolling over: if it detects a drop in temperature it can reduce the torque on its wheels to prepare for travelling over ice. A robot designed to fight fires could use a temperature sensor to direct itself to the hottest parts of a burning building, where it will be most effective.

**Light**

Another detectable property of the environment is light. One use is for robots who have different tasks to accomplish at night than in the day: a robot can detect decreasing light and change its behaviour into night mode. Changes in light can also indicate a change in surroundings: a robot designed to explore houses in disaster zones could use it to navigate around a home that has collapsed, by directing itself towards the light to get out of tight spaces.

**Sound**

A sound sensor will detect the presence of sound and also measure the amplitude of the sound. The higher the amplitude, the louder the noise. This could be used by a robot designed to study wildlife, by following noises and sounds where they are more intense. A more complex use could a sound sensor for speech recognition, responding to commands spoken by a user.

**Chemical**

Certain chemical properties can be measured by a robot using sensors. *pH* sensors detect the acidity/alkalinity of the environment around a robot. Scientific robots could use this to check the quality of rivers or soil in remote places. Carbon Monoxide sensors can be used to explore hostile environments where human explorers would be put at risk.

### Object proximity

Mobile robots have to navigate the world around them, often autonomously, and there are sensors that help them detect the proximity of other objects around them.

**Infrared Sensors**

One method of detecting objects around a robot, is the use of an infrared sensor. Infrared sensors detect changes in the levels of environmental infrared radiation, which is given off by objects that are hot (particularly living things). They are not very effective at detecting inanimate objects.

**Ultrasonic Distance Sensors**

A better sensor for robots that have to navigate around inanimate objects, is the UDS (ultrasonic distance sensor). These sensors emit high frequency noises, which rebound off of objects in the surrounding area and return to the robot. The gap between the emission and the return of the sound can be used to calculate the distance between the robot and the object that the sound bounced off of. This is exactly how bats see the world when flying at night.

I am going to show you how to use a UDS in your buggy, and in the next step you will see how they work in greater detail.

### Sense your way.

**Pick one of the types of sensor you have seen in this step.**

**Think of another use of that sensor in robotics, either from your past experience or by using your imagination**

Share your ideas in the comments section.
