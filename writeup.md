# **Path Planning** 

Path planning system for highway driving

## Writeup

---

**Build a Path Planning Project**

The goals / steps of this project are the following:
* The car is able to drive at least 4.32 miles without incident
* The car drives according to the speed limit
* Max Acceleration and Jerk are not Exceeded
* Car does not have collisions
* The car stays in its lane, except for the time between changing lanes
* The car is able to change lanes

#### 1. The car is able to drive without incident

Instead of using cost functions and finite sate machines, I decided to implement a simpler code structure to achieve this goal. By using the sensor fusion data, and estimation of where other vehicles on the road would be in the next time frames, we could avoid collision. I utilized a series of conditions for changing lanes or reducing the speed when a vehicle is in our lane to achieve this goal.

#### 2. The car drives according to the speed limit

By Defining the maximum velocity to be a little lower than the speed limit, and imposing this limitation in all conditions, this goal is achieved.

#### 3. Max Acceleration and Jerk are not Exceeded

Acceleration is set to be about 5 m/s in order to perform smooth velocity change in either increasing the velocity or decreasing it. it also limits the jerk at the start where the car needs to increase its speed from zero to the speed limit.
Jerk is also needed to be control where the vehicle turns. This problem was solved by using the spline library and finding a smooth trajectory for next time intervals.

#### 4. Car does not have collisions

There are two situations that our car may have a collision. The first one is where other vehicles in our lane are moving with slower speed. To address this problem, I used the sensor fusion data to locate other vehicles in our lane and reduce the velocity to avoid accident.
The second situation is where we need to change lane. I decided to calculate the absolute value of the distance between other vehicles and the ego vehicle, and allow lane changes in case there is safe gape both in front and behind. There were situations in the test run that leaded to an accident due to lane change with out considering the distance to other cars that are behind.

#### 5. The car stays in its lane, except for the time between changing lanes

As the car d-coordinate in frenet space is used to define each lane, the car stays in the center of its lane unless where change lane is required.

#### 6. The car is able to change lanes

As I described before the car is able to change lane to keep the maximum velocity by using sensor fusion data, and calculating the distance to other cars. 
The lane change process is performing by finding a spline that fits to the points in which the car is located and the point it is going to reach in the future.
