# Changing the number of signals

The number of devices available for each signal is defined in the [top file](https://github.com/mufpga/MicroFPGA/blob/7908fc16b8069504b6fcd9e3213126e55c3c6d61/Au%2B/source/au_plus_top.luc#L68) of the AlchitryLabs project. Note that the number of analog signals cannot be increased (technically only to 9 if incorporating the dedicated VP/VN signal).

1. First, change the constants at the beginning of the [top file](https://github.com/mufpga/MicroFPGA/blob/7908fc16b8069504b6fcd9e3213126e55c3c6d61/Au%2B/source/au_plus_top.luc#L68) (line 62):

   ```verilog
   // number of signals
   const NUM_LASERS = 8;
   const NUM_TTL = 5; // we added one TTL signal here
   const NUM_PWM = 5;
   const NUM_SERVOS = 7;
   const NUM_ANALOG = 8;
   ```

2. Then, add the corresponding signals to the definition of the top file module (lines 34). Here is an example of the new TTL signal:

   ```verilog
   output ttl3,
   output ttl4, // new ttl signal
   output servo0,
   output servo1,
   ```
   
   Ignore the error for now.
   
3. Finally, the new signal should be linked with a module output. In our example (line 226):

   ```verilog
   ttl3 = ttl.q[3];
   ttl4 = ttl.q[4]; // new ttl signal receives the output of the ttl module
   ```
   
4. Finally, the new signal of our example (ttl5) needs to be added to the [user constraint file](https://github.com/mufpga/MicroFPGA/blob/7908fc16b8069504b6fcd9e3213126e55c3c6d61/Au%2B/constraint/user.acf#L16):

   ```verilog
   pin ttl3 A8;
   pin ttl4 C40; // new ttl
   ```
   
   Here, we chose a free 3.3 V pin (see [pins mapping](resource3_pins_br.md)).
   
5. Then compile and update the firmware (see [building MicroFPGA configuration](2_installing_microfpga.md) for a walkthrough). 

Note that if you are using Micro-Manager, the Java or Python libraries, you will have to modify the number of signals in the user code as well:

- [Micro-Manager device adapter](https://github.com/mufpga/MicroFPGA-mm/blob/ec88b570e533122c0ce0223c18f39edf68f77a3a/MicroFPGA.cpp#L41)
- [Python library](https://github.com/mufpga/MicroFPGA-py/blob/2f455be3fdba87c680d4ca336b69d2ad7faa5268/microfpga/signals.py#L5)
- [Java library](https://github.com/mufpga/MicroFPGA-java/blob/766051054e9982a18474cf43dd8a4cfb13994a76/src/main/java/de/embl/rieslab/microfpga/devices/Signal.java#L7)

