### Servo

Servos typically require three signals: power, ground and position. We advise supplying the power with another device than the FPGA to avoid drawing too little current, while connecting the source ground to the FPGA.

A [servo position signal](https://en.wikipedia.org/wiki/Servo_control "Wikipedia Servo control") is usually a PWM signal between 1ms and 2 ms, with a period of 20 ms. MicroFPGA follows this standard with a pulse width resolution of 16 bits:

| Position | Value |
| :------: | :---: |
| Minimum  |   0   |
| Maximum  | 65535 |

Additionally, MicroFPGA turns off the servo signal after 10 seconds in order to avoid vibrations on the optical table.

### 