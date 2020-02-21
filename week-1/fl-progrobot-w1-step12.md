[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Why we call robotics challenging

You are coming to the end of the first week of your journey into the world of robotics, and you may have noticed that working in this area requires you to navigate some challenges! Robotics is a complex and vast subject, which can be off-putting when you are starting out. I want to discuss some of these challenges and hear how you have overcome them.

### Challenges with components

![A robot buggy, with wheels and a face. Some loose cables are poking out from the top of the bot. Its expression looks dazed and confused](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Illustration/18-1_12-Loose_Cables.png)

#### Jumper cables and loose components

The jumper cables you have been using for the buggy so far have a tendency to come loose from the components or GPIO pins if you knock them. I cannot tell you how many times I have been pulling my hair out trying to find an error in my code, only to find that it was a loose jumper cable causing the problem.

#### GPIO pin numbers are weird

The numbering on the GPIO pins can be confusing; they are numbered as the processor sees them, rather than as they are laid out on the board. This is a product of wanting the Raspberry Pi to be backwards-compatible as much as possible; when the pins changed from a 26-pin to a 40-pin set-up they had to be rearranged, and the original pins were moved and mixed with new ones.

#### Debugging components

A lot of the things you have done this week will be completely new to you, as will the components you are using. Dealing with components rather than products means you forgo some of the hand-holding that comes with a pre-built device.

![A person holding at an ultrasonic distance sensor looking confused by the device](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Illustration/19-1_12-Confusing_Component.png)

When you buy components, you have to figure out how they work and test them. If the components are new to you, this can be a challenging process, as you don't know what to look for, or how to test the component.

#### Cardboard is easy, not strong

As you create your buggy, you are most likely using cardboard to house it; this is great, and the most sensible option for the initial build. This, however, brings its own challenges; as previously mentioned, the components are susceptible to being knocked out of place. These two challenges combined mean that as roboticists we need to do two things when testing: check the components after each run, and make sure to avoid bumps as much as possible.

Things can go wrong if the placement of your components in the chassis doesn't allow for particularly sturdy attachments; even a small bump can knock any number of components loose, and you may need to do a thorough check to find out what is going wrong. 

### The environment

#### Not all floors are created equal

Creating a mobile robot, particularly one that uses wheels to navigate around, requires you to consider carefully the floor you test it on.

![Three robots stuck on a carpet floor which look sad, confused and struggling to move](https://rpf-futurelearn.s3-eu-west-1.amazonaws.com/Robotics+-+Robot+Buggy/Illustration/20_1_12-Wobbly_Floor.png)

Some motors have no problem navigating carpet, linoleum, or tiles; others will not work on anything other than smooth concrete. This can cause frustration, as you may adjust the settings on the wheels, only to find out it was an uneven floor causing the issues.

#### Environments are not consistent

Some of the sensors and components you will use can be greatly impacted by the environment you test the buggy in. Light and line sensors can be thrown off by environmental light levels and have to be calibrated in order to be accurate. Handling these inconsistencies is much simpler if you are working with components that you are familiar with. This process can cause considerable frustration if you are having to learn how to calibrate the sensors at the same time.

### It's not you, it's robotics

I hope you have found some comfort in this step. This is a challenging area of computing, and you are not alone in coming across frustrations when working on your buggy.

### Discussion

Think of a challenge you have faced during this first week. It could be one from the areas I have discussed here, or another challenge that you would like to discuss.

What happened? How did you overcome the challenge? If you haven't yet, this is a great time to ask for help!

If you haven't experienced these challenges, what have you done to prevent them? Could you share your process, to help other learners?

Share your challenges and stories in the comments below. We are all in this together, after all; it may be frustrating, but together we can overcome these obstacles and create amazing robots.
