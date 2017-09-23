# Research_ADAMS_Sim
This is just a log for my work in ADAMS Simulation. It helps me keep track of things.

# LOG
## 20170923
### reopen *params_match_real_device.bin* but made no changes
new block was put into the Simulink assembly but didn't work

there was a strange offset in joint 1 and 3

changed the setup to run xuan's motion to check the initial pose measurements

discovered there was a new offset for joint 1 and 3

could be b/c the design params changes or my measurements are sensible to params changes

saved nothing and compensated new offsets in Simulink model

**Note:** check everytime when the design params are changed

**Note:** the unit for ADAMS model might not be as clear. the angle measurements should be in degrees but they were in rads. I have to check again about torques, Nm or Nmm.

## 20170919
### save *test_controlblock_whole.bin* as *params_match_real_device.bin*
rewrote the IK just to clarify things and have it as a math model

compared this math model with ADAMS model and realized the params for the two are not the same

(no wonder the measurements were off and all)

(how should I explain this to my supervisors, because I'm stupid?)

this was the file to update the params in the ADAMS model to match that in the real device

now, math model, ADAMS model, and the real device should be the same (of the same params setup)

because the TCP was moved due to change of params, I redefined hand motion

with the help from Xuan, the motion now would change with the model

generated 2 Simulink Model from ADAMS

*realHDwG:* real haptic device with gravity, this would be the main version from now on

*realHDwoG:* without gravity, feel like it might be useful

### TODO:
assumed everything moved with the model, need to check

there was an offset between the point "TCP" in math model and ADAMS model, choose one (due to universal joint instead of ball joint)

(20170923) kinda solved this by using a F/T transformation formula. have to keep looking

~~put the new ADAMS block into the Simulink assembly and test~~

(20170923) it's working now. see related log.

## 20170916
### reopened *drive_with_force.bin* but made no changes
since I successfully rendered a force along z axis, those motor torques should give me a good estimation about directions

checked all the motor torque splines and flipped the direction of motor 1 in simulink

the scope looked better but still there were undesired F/Ts

I also lowered the stiffness of the wall, otherwise, a small error could be magnified like a wrong measurement

**NOTE:** there could be position errors in all directions

**maybe I should start something like this for Simulink Models as well**

## 20170914
### reopened *drive_with_force.bin* but made no changes
confirmed the F/T on hand in free space at the origin point with ADAMS model

the Simulink result was the same, meaning the measurements were OK

### TODO:
make sense of the present measurements (may lead to the next item)

double check if the direction of torque on motors were correct

(20170916) flip motor 1. motor 5 might also need to be flipped.

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
