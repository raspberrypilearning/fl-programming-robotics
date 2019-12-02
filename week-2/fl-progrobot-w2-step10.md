[comment]: # (
Is this step open? Y/N
If so, short description of this step:
Related links:
Related files:
)

## 


### The algorithm

Whenever you embark on coding a solution to a problem, you need to first spend some time thinking about the intentions of the program and how you might achieve these outcomes. 

The algorithm you will need to create for detecting and navigating around an object needs breaking down first into several parts, which I am going to pose as questions:

+ What hardware do I need to access within my program and what libraries do these rely on?
+ At what distance is an object too close to the buggy?
+ What should happen once an object has been detected as being too close?
+ How often will you check whether an object is too close or not?



The two pieces of hardware I will need to communicate with to move the buggy and avoid an obstacle are the UDS and the motors. 


Begin by creating a new file. You can use the code previously written during this course to help you throughout this program.

 
The GPIO Zero library has been utilised throughout this course to interact with two of the buggy's components; `Robot` to control the motors and `InputDevice` and `OutputDevice` for the UDS.

Your program will also need to use `time` and `sleep` from the time library to calculate the distance between the UDS and an object.


Currently, the program calculates the time taken from a sound being emitted by the UDS until that sound is detected. 

Now you need to figure out what distance an object should be in front of the buggy before enacting the next stage of the algorithm. I'm going to choose 20cm (or 0.2 metres) as my threshold value for now and I can experiment with this value later.
