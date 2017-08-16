# Path-Planning-Project
## Objective
Implementing a Path Planner to drive a car in Udacity simulator

## Requirements
1-The car drives according to the speed limit (50 Mph)
2-The car does not exceed a total acceleration of 10 m/s^2 and a jerk of 10 m/s^3.\
3-The car does not collide with any other car
4-The car stays inside one of the 3 lanes on the right hand side of the road and change lanes in at most 3 seconds.

## Results
The car is able to drive around the track satisfying all the requirements mentioned above 

## Methodology
The output of the path planner is to provide a list of waypoints to be tracked by the controller. Below is a description of how this path is generated.

**The path consists of 50 waypoints**
2-The first set of waypoints are the the waypoints of the previous path which were not executed as shown in lines 417->419
3-The rest of the 50 waypoints are sampled from a polynomial, this polynomial is generated using 5 waypoints(the last 2 waypoints in the previous path, and 3 points generated from the last executed waypoint) this part is implemented in lines 363 -> 441. Specifically, in lines 417->420 previous waypoints are added, in lines 427->442 the rest of the waypoints are sampled from the polynomial and added, in lines 363->410 the polynomial is fitted with the 5 points mentioned above.

**Lane Changes**
1-The car changes it's lane when there is a car infront which is slower, and it's safe to change lanes.
2-Left lanes are preferable than right lanes, so if a car infront is slower and the left lane is safe, the car will move to the left lane. If the left lane is not safe the car will move to the right lane if it is safe.
3- This part is implemented in lines 277->365. Specifically, in lines 277->292 we check if a front car is moving slowly. If that's true we evaluate the safety of left lane in lines 301->328 and if it is not safe, we evaluate right lane safety in lines 331->356

## TODO
1-Refactor code and encapsulate the main code in a Path Planner Class
2-if it's ok to changed to both adjacent lanes, calculate a cost function for each one of them and choose the lane change with least cost.
