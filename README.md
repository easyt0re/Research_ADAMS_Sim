# Research_ADAMS_Sim
This is just a log for my work in ADAMS Simulation. It helps me keep track of things.

# LOG
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

