# Research_ADAMS_Sim
This is just a log for my work in ADAMS Simulation. It helps me keep track of things.

# LOG
## 20170914
### reopened *drive_with_force.bin* but made no changes
confirmed the F/T on hand in free space at the origin point with ADAMS model

the Simulink result was the same, meaning the measurements were OK

### TODO:
make sense of the present measurements (may lead to the next item)

double check if the direction of torque on motors were correct

there was no motor model or gear ratio in Simulink right now

## 20170912
### save *test_motor_torque_sensors.bin* as *test_controlblock_whole.bin*
I think so far, the model is capable of the whole procedure

This is an attempt to generate the Simulink block for co-simulation
- deactivate all the unrelated motion, measurements, and F/T
- establish measurements on hand w.r.t world frame

the newly generated control related things are *Control_Plant_2*,
this is the whole control plant block with both pathways

I made mistakes in a few I/Os so *Control_Plant_2* was abandoned and deleted

regenerated files are *whole_plant_bothway*

I copied all the newly generated files to the Simulink folder

the old *Control_Plant_1* is only the forward (position) pathway

the model would not work after a simple assembly

I realized I never align all the origins in different systems

I went back to test with the forward pathway with forward kinematics (FK)

I created transformation blocks to compensate offsets

**NOTE:** the model seemed to have a drift in TraY

~~I tried to make sense of the measurements to make sure they were properly aligned~~

it actually kinda worked

**some of these logs are Simulink related**

## 20170907
### save *test_motor_torque_sensors.bin* as *test_gravity_compensation_capability.bin*

this is an attempt trying to compensate "everything"

the whole procedure would look like this:

- drive with TCP to obtain joint motion splines
- drive with motors to obtain joint torque splines
- drive with TCP again with compensation from those splines
- take measurements on "hand" when drive with TCP, the second one should be zero

the result looked promising yet confusing

I managed to make F/T on hand (if correct) very close to zero with compensation

but the problem was, it's already close to zero without compensation

this could be correct, since the hand is giving F/T at a far side

like, you are lifting a bar at one side and the rotation point is at the other side

**Note:** the measurements on hand were w.r.t the world frame right now, it could be wrong

**Note:** the measurements on hand were w.r.t the hand frame in **drive_with_force.bin**

given the speed of this "estimation", this could be a strategy to compensate "everything", if we really need one

there is still a possibility that "gravity compensation" is done automatically


## 20170906
### repurpose *test_motor_torque_sensors.bin* to test what should be the right way to measure joint torques

the current question is: what are we really measuring? we have to find a right way and stick to it

changed all torque measurements, from measure **joint** to measure **joint_motion**

changed all the measurements to Z component (rotation axis) and w.r.t local coordinate system (joint_axis)

**At this point I started to wonder what I did and how that's useful.**

zero-gravity test was also done in this file

this gave me some confirmation about sensors' correctness and proof that there were inertial f/t

on the motors the torque with gravity is almost 100 times the torque without



### save *test_motor_torque_sensors.bin* as *drive_with_force.bin*

this is not really actuating the whole system with torque only and I doubt that would work

the scenario is to render a force at a fixed point

first, motor-driven, fixed at origin for a while

in the meantime, put a growing force at TCP, point to hand

save motor torque splines for later

next, TCP driven, create measures for those motion

apply those splines and see if we could recreate the force

there are some small drift (noise) but I think it's proved to be basically working

## 20170903
### save *new_ang_measure.bin* as *test_motor_torque_sensors.bin*

try to see how the motor torque sensors work

try to see what would happen if drive the joints with both motor (position) and torque

we know that when the active part is different (TCP or motors), motor torque measurements differ

set motor active and measure motor torque

save these as splines and apply them while motor active

### TODO:
~~find a way to measure the F/T on TCP when motor torque is active~~

(20170914) see *drive_with_force.bin*, done


## 20170901 
initiate this directory

### save *new_motion.bin* as *new_ang_measure.bin*

try to have fixed def for angle's direction and bias 

the goal was to switch the splines only and the simulation worked correctly

change the measures to function measurements, f(t)

### TODO:
automate this whole process

~~try to figure out the torque_measuremnets on motors~~

~~if possible, does that mean F/T on TCP is also possible?~~

(20170914) see *test_motor_torque_sensors.bin* and *drive_with_force.bin*, done
