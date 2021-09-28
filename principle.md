# MicroFPGA

MicroFPGA is an electronic platform generating signals that are commonly needed when controlling a microscope. It is based on the Au and Cu FPGAs (Alchitry).

The available signals are the following:

| Name            | I/O    | Function                                                     | Default number |
| --------------- | ------ | :----------------------------------------------------------- | :------------: |
| Laser trigger   | Output | Triggering lasers based on the processing of an input camera signal. Can be used for pattern triggering or microsecond pulsing of lasers. |       8        |
| TTL             | Output | TTL signals are either HIGH or LOW, and can be used to control devices such as flip-mirrors or switches. |       5        |
| Servo           | Output | Servos signals are periodic digital signals (20 ms period and 1 to 2 ms pulses) used commonly to move servomotors. The MicroFPGA servo signals are turned off after 10 ms in order to prevent vibrations. |       7        |
| PWM             | Output | PWM signals are similar to the Servo signals, except they are not switched off after 10 s. Together with a low-pass electronic filter, they can be used to produce analog signals, used for instance with AOTFs. |       5        |
| Analog read-out | Input  | Analog inputs are limited to 0-1 V and can be used to monitor signals from the microscope, e.g. temperature, laser position, laser power... |   8 (fixed)    |



**GENERAL FIGURE here**


