### Servomotor

Servomotors are 

![flip_mount_small](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Flip_mount/flip_mount_small.JPG)![3D_printed_fw_small](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Filter_wheel/3D_printed_fw_small.JPG)![rail_servo_small](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Linear_stage/rail_servo_small.JPG)

Servomotors typically require three signals: power, ground and position. We advise supplying the power with a device other than the FPGA to avoid drawing too little current. The ground signal should also be connected with the ground from both source and FPGA.

A [servo position signal](https://en.wikipedia.org/wiki/Servo_control "Wikipedia Servo control") is commonly a PWM signal with pulse length ranging from 1ms to 2 ms, and with a period of 20 ms. MicroFPGA follows this standard with a pulse width resolution of 16 bits:

| Parameter |  Range  |           Value           |
| :-------: | :-----: | :-----------------------: |
| Position  | 0-65535 | 1 ms to 2 ms pulse length |

Additionally, MicroFPGA turns off the servo signal after 10 seconds in order to avoid vibrations on the optical table.

In order to change the pulse range, for instance to accommodate an unconventional servomotor, it is necessary to change MicroFPGA code and recompile it. The same applies to changing the time-out duration before switching off the signal. In both cases, a [tutorial is available](tuto7_servo.md).

