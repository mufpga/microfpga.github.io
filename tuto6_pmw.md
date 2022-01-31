## Change PWM bit depth

The PWM level is currently encoded by a 8 bits value. To increase the number of steps between the minimum and maximum value, the encoding can be changed to 16 bits for instance.

1. In au_plus_top.luc (line 139), change the bit depth to 16:

   ```verilog
   pwm pulsewm[NUM_PWM](#TOP(254),#DIV(9),#WIDTH(16));
   dff dutycycle[NUM_PWM][16];
   ```

2. In au_top.luc (line 189), change the bit depth to 16:

   ```verilog
   dutycycle.d[reg.regOut.address-ADDR_PWM] = reg.regOut.data[15:0];
   ```

Now, the code on the user side should be changed to accept higher values, for instance:

- [Micro-Manager device adapter](https://github.com/mufpga/MicroFPGA-mm/blob/ec88b570e533122c0ce0223c18f39edf68f77a3a/MicroFPGA.cpp#L1642)
- [Python library](https://github.com/mufpga/MicroFPGA-py/blob/2f455be3fdba87c680d4ca336b69d2ad7faa5268/microfpga/signals.py#L42)
- [Java library](https://github.com/mufpga/MicroFPGA-java/blob/766051054e9982a18474cf43dd8a4cfb13994a76/src/main/java/de/embl/rieslab/microfpga/devices/PWM.java#L7)



