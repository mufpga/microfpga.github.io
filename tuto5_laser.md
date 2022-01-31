## Change laser duration step

Currently, the laser pulse duration is in microseconds. In order to change the step size, refer to the [laser_trigger.luc file](https://github.com/mufpga/MicroFPGA/blob/7908fc16b8069504b6fcd9e3213126e55c3c6d61/Au%2B/source/laser_trigger.luc#L40) of the firmware (line 40):

```verilog
const NM_CYCLES = 100; // convert to ~us
```

Since the Alchitry FPGAs have an internal clock of frequency 100MHz, each clock cycle takes about 1/100 us. If we wanted to have a step size for the pulse duration of 100 ns, then line 40 becomes:

```verilog
const NM_CYCLES = 10;
```
The firmware then needs to be compiled and updated on the FPGA.

**Important note**: If you increase `NM_CYCLES`, you need to update the counter, to make sure that it can count more cycles than the maximum duration d times `NM_CYCLES`: `max(c)>d*NM_CYCLES`. By default the pulse duration is 16 bits, which means that the counter needs to go as high as `(2^16-1)*NM_CYCLES`. For `NM_CYCLES=1000`, the counter does not need to be changed, usually by increasing the number of bits by one. The number of bits need to be `x > log2((2^16-1)*NM_COUNTER+1)`, which means larger than 26.


## Change laser duration maximum

The laser pulse duration is encoded by a 16 bits value. The maximum value is therefore 65535 us pulse length by default. However, the register interface allows values up to 32 bits to be transferred. Therefore, the code can be easily modified to accommodate the whole bit depth, with a new maximum of 429'496'7295. If you follow the previous section with NM_CYCLES=1, this leads to a maximum pulse length of about 43 seconds.

1. In au_top.luc (line 116), change the bit depth to 32:

   ```verilog
   dff duration[NUM_LASERS][32];
   ```

2. In au_top.luc (line 180), change the bit depth to 32:

   ```verilog
   duration.d[reg.regOut.address-ADDR_DUR] = reg.regOut.data[31:0]; 
   ```
   
3. In laser_trigger.luc (line 28), change the bit depth to 32:

   ```verilog
   input dura[32],
   ```
   
4. In laser_trigger.luc (line 47), adjust the bit depth of counter (see previous section):

   ```verilog
   dff count_sig[x]; // x > log2((2^16-1)*NM_COUNTER+1
   ```

Now, the code on the user side should be changed to accept higher values, for instance:

- [Micro-Manager](https://github.com/mufpga/MicroFPGA-mm/blob/ec88b570e533122c0ce0223c18f39edf68f77a3a/MicroFPGA.cpp#L999): line 477, replace 65535 by 4294967295.
- [Java](https://github.com/mufpga/MicroFPGA-java/blob/766051054e9982a18474cf43dd8a4cfb13994a76/src/main/java/de/embl/rieslab/microfpga/devices/LaserTrigger.java#L147): line 147.
- [Python](https://github.com/mufpga/MicroFPGA-py/blob/2f455be3fdba87c680d4ca336b69d2ad7faa5268/microfpga/signals.py#L38): line 38.

**Important note**: the error code for MicroFPGA is defined in au_plus_top.luc (line 97):

```verilog
const ERROR_UNKNOW_COMMAND = 11206655; 
```

When changing any parameter from 16 bits to 32 bits, reading out the parameter value while it is equal to 11206655 will cause the Micro-Manager device adapter or the Java and Python libraries to produce an error. Indeed, this value will be interpreted as an wrong address request.
