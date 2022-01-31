
# MicroFPGA principle

MicroFPGA is based on the Au, Au+ and Cu FPGAs from [Alchitry](https://alchitry.com/). Once configured, the FPGA is capable of generating a certain number of signals, as well as reading analog inputs (Au and Au+). It has been used with a [variety of devices](resource5_applications.md) on multiple microscopes.

**SUMMARY FIGURE**

The MicroFPGA project is split between multiple Github repositories:

- [FPGA configuration](https://github.com/mufpga/MicroFPGA)
- [Complementary electronics](https://github.com/mufpga/MicroFPGA-electronics)
- [Micro-Manager device adapter](https://github.com/mufpga/MicroFPGA-mm)
- [Java library](https://github.com/mufpga/MicroFPGA-java)
- [Python package](https://github.com/mufpga/MicroFPGA-py)
- [LabView library](https://github.com/mufpga/MicroFPGA-labview)

Click on the various available signals in order to access more detailed descriptions:

| Name                                   | I/O         | Summary                                                      | Default number |
| -------------------------------------- | ----------- | :----------------------------------------------------------- | :------------: |
| [Camera trigger](principle_trigger.md) | Input/Ouput | In PASSIVE mode, the FPGA receives a signal from the camera in order to trigger the lasers, in ACTIVE mode it generates a fire signal for the camera and can trigger the lasers similarly to the PASSIVE mode. |   1 (fixed)    |
| [Laser trigger](principle_trigger.md)  | Output      | Triggering lasers based on the processing of an exposure signal. Can be used for pattern triggering and/or laser pulsing. |       8        |
| [TTL](principle_ttl.md)                | Output      | TTL signals are either HIGH or LOW, and can be used to control devices such as flip-mirrors or switches. |       4        |
| [Servo](principle_servo.md)            | Output      | Servos signals are periodic digital signals (20 ms period and 1 to 2 ms pulses) used commonly to move servomotors. The MicroFPGA servo signals are turned off after 10 ms in order to prevent vibrations. |       7        |
| [PWM](principle_pwm.md)                | Output      | PWM signals are similar to the Servo signals, except they are not switched off after 10 s. Together with a low-pass electronic filter, they can be used to produce analog signals, used for instance with AOTFs. |       5        |
| [Analog](principle_ai.md)              | Input       | Analog inputs are limited to 0-1 V and can be used to monitor signals from the microscope, e.g. temperature, laser position, laser power etc. |   8 (fixed)    |
