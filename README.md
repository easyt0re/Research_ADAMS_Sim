# Research_ADAMS_Sim
This is just a log for my work in ADAMS Simulation. It helps me keep track of things.

# LOG
## 20170906
repurpose **test_motor_torque_sensors.bin** to test what should be the right way to measure joint torques

the current question is: what are we really measuring? we have to find a right way and stick to it

changed all torque measurements, from measure **joint** to measure **joint_motion**

changed all the measurements to Z component (rotation axis) and w.r.t local coordinate system (joint_axis)

**At this point I started to wonder what I did and how that's useful.**



save **test_motor_torque_sensors.bin** as **drive_with_force.bin**

this is not really actuating the whole system with torque only and I doubt that would work

the scenario is to render a force at a fixed point

first, motor-driven, fixed at origin for a while

in the meantime, put a growing force at TCP, point to hand

save motor torque splines for later

next, TCP driven, create measures for those motion

apply those splines and see if we could recreate the force

there are some small drift but I think it's proved to be basically working

## 20170903
save **new_ang_measure.bin** as **test_motor_torque_sensors.bin**

try to see how the motor torque sensors work

try to see what would happen if drive the joints with both motor (position) and torque

we know that when the active part is different (TCP or motors), motor torque measurements differ

set motor active and measure motor torque

save these as splines and apply them while motor active

### TODO:
find a way to measure the F/T on TCP when motor torque is active


## 20170901 
initiate this directory

save **new_motion.bin** as **new_ang_measure.bin**

try to have fixed def for angle's direction and bias 

the goal was to switch the splines only and the simulation worked correctly

change the measures to function measurements, f(t)

### TODO:
automate this whole process

try to figure out the torque_measuremnets on motors

if possible, does that mean F/T on TCP is also possible?

