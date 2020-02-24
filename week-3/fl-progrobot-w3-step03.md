[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## Line-sensing robots

This week you will be attaching a line sensor to your buggy and turning it into a line-following robot. This type of robot is very popular with beginner roboticists, as it lets you experience both the software and hardware aspects of robotics. However, line-following robots are much more than a learning tool, and have a rich history going all the way back to the 1960s.

### What is line sensing and why are robots doing it?

Line-sensing robots (sometimes called line-following robots) move autonomously by following a line, typically one drawn on the ground underneath the robot.

In early robotics, line following was a way of allowing robots to move autonomously. Processors at the time were struggling to handle the amount of data required from cameras or proximity sensors for full autonomous movement. Line sensing was pursued as an achievable alternative to true autonomous movement.

### Examples of line-sensing robots

As you have heard already, robots are often used to explore harsh environments that would be difficult for human explorers. In the 1960s, one of the biggest exploration projects of all time was in full swing: the space race. Most robots that were built for Moon landings were remote-controlled. The massive distance between the Earth and the Moon meant that these early Moon buggies had to deal with huge delays between instruction and action.

To try to tackle this challenge, a team of university roboticists at Stanford created a cart.

![](images/3_3_Stanford_Cart.png)

#### The Stanford Cart

The Stanford Cart started life as a remote-controlled mobile robot. A four-wheeled cart, its chassis consisted of a rectangular box fitted with cameras and an on-board TV system. Researchers at the university worked on the cart from 1960 to 1980; for a period in 1970 they outfitted the cart with line sensors to test autonomous navigation algorithms.

[Here is a video of the robot](https://youtu.be/8Mxk2L3lu9Q) following a white line on the ground.

[Here is another](https://exhibits.stanford.edu/ai/catalog/jk541kq7003); the outtakes from the original video start from six seconds in.

The robot used a camera pointing towards the ground, which tracked a white line drawn by the researchers. The robot would adjust its direction to keep the line in the middle of the picture captured by the camera. It moved at a walking pace and was reasonably successful at this task.

Later, the cart would be turned into a fully autonomous vehicle; for a time, it was at the cutting edge of vision-controlled robots. The team would famously let the robot roam the campus unaccompanied, and created a sign that read "CAUTION ROBOT VEHICLE" to hang on it when it was out and about. This sign caused the lead researcher a lot of headaches, as he kept having to get it remade after it was repeatedly stolen.

### Modern uses for line-following robots

Line-following robots excel in situations in which the tasks they need to complete do not involve complex movement or much decision-making.

#### Warehouse robots

A good example is robots working in a warehouse; the movements they need to make require them to follow preset paths to collect pallets. Warehouses, particularly those of large internet shopping companies (think Amazon or Alibaba), need a lot of stock to be moved around the massive buildings. The stock robots move around the warehouses to pick up cages containing items that have either just arrived or are being prepared for dispatch. Lines on the floor allow the robots to navigate the busy warehouse space without wasting too much computational power on navigation. 

#### Competitions

As mentioned earlier, line-sensing robots have a secure place in the robotics world, as they make a great challenge for beginner roboticists.

This has led to the creation of competitions pitting robots against one another, challenging them to follow a line track as quickly as possible. Judges watch the robots and penalise them for straying from the line, either by giving time penalties or in some cases by disqualifying them.

The size and complexity of the track depends on the competitors and their expected experience levels. Some competitions are aimed at children, and so the courses are simple, small ovals. Some more complex competitions involve line mazes for robots to map and navigate.

Have a look online; you might be able to find a competition running near you. You could even enter your buggy!

### Discussion

Earlier, I discussed warehouse robots, which are one modern use of line following.

What other types of work could a line-following robot do? Are there other types of work that require only simple navigation?

Leave your thoughts in the comments below.
