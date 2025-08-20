# MultiAgentControlSystems
#### Development of multi-agent control systems based on reinforcement learning

I have simulated a multi-agent control of quadrotors without using reinforcement learning algorithms (non-intelligent approach) in Simulink 2023b.
Here's a summary of what I've done so far:

## Project Description
This project contains the simulation of a Multi-Agent control of Quadrotors. The Quadrotors have a 6-DOF nonlinear dynamics controlled with the Sliding-mode controller. The Simulation is done with the 2023b version of the Simulink software.

The Simulink file contains 3 main subsystems:

### Subsystem 1: Desired Path

Where the reference path as a function of time is planned here. It consists of 3 phases:

1- Climb to gain enough altitude up to 5 meters.

2- Perform a cruise flight for a while at a constant altitude.

3- Perform a Helical maneuver along the Z axis.


### Subsystem 2: Path Following and Obstacle Avoidance 


The reference path and its derivatives are the inputs of this subsystem.

The reference path is given to the leader to follow with a PD controller, while avoiding obstacles.

The Leader's path is given to the followers to follow the leader, while:

1- Maintaining a safe distance between each other (Swarming),

2- Avoiding static and dynamic obstacles.

3- making a pentagonal formation.

4- Time-limited formation change to linear/pentagonal wherever needed.

Note: This subsystem considers the agents as a point mass with two-integrator dynamics, and its outputs can be used for any control plant with different dynamics.



### Subsystem 3: The Agents 

This subsystem includes five agents, the leader at the front, and 4 agents as followers. They receive their reference path from the previously mentioned subsystem, compare it to their current states, and are controlled by the SMC controller, which produces the 4 outputs (z-axis Thrust, and three torques along x-y-z axes) needed to control this underactuated system. Next, these forces and momentums are converted to rpm of motors, considering a sinusoidal disturbance. Before these RPMs are sent to the nonlinear dynamic model of the quadrotor, actuator dynamics, delay, and saturation are added by their respective blocks.
