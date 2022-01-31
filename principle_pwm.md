### Pulse-width modulation

[PWM signals](https://en.wikipedia.org/wiki/Pulse-width_modulation) are useful signals that encode values in the duty cycle of a periodic signal. A typical use of PWM signals is the control of [servomotors](principle_servo.md). However, PWM signals can also be low-pass filtered in order to obtain an analog signal. That way, the PWM duty cycle directly translates into a voltage level. The [SCB board](resource1_electronics.md) allows to perform this conversion using MicroFPGA PWM signals.

As opposed to the servomotor signals, MicroFPGA PWM signals are not switched off. They are defined using only 8 bits values (0-255) to set the duty cycle value. The period of the signal is 1.3 ms.

| Parameter | Range | Value  |
| :-------: | :---: | :----: |
|   State   | 0-255 | 0-100% |

