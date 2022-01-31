# Changing addresses

Addresses in MicroFPGA [register Interface](resource2_communication.md) are defined in the [top file](https://github.com/mufpga/MicroFPGA/blob/7908fc16b8069504b6fcd9e3213126e55c3c6d61/Au%2B/source/au_plus_top.luc#L74) of the AlchitryLabs project. In order to modify them in the firmware, change the address constants (line 74 to line 92):

```verilog
  const ADDR_MODE = 0; 
  const ADDR_DUR = NUM_LASERS; // 8
  const ADDR_SEQ = ADDR_DUR+NUM_LASERS; // 16
  const ADDR_TTL = ADDR_SEQ+NUM_LASERS; // 24
  const ADDR_SERVOS = ADDR_TTL+NUM_TTL; // 28
  const ADDR_PWM = ADDR_SERVOS+NUM_SERVOS; // 35
  
  const ADDR_ACTIVE_TRIGGER = ADDR_PWM+NUM_PWM; // 40
  const ADDR_START_TRIGGER = ADDR_ACTIVE_TRIGGER+1; // 41
  const ADDR_CAM_PULSE = ADDR_START_TRIGGER+1; // 42
  const ADDR_CAM_PERIOD = ADDR_CAM_PULSE+1; // 43
  const ADDR_CAM_EXPO = ADDR_CAM_PERIOD+1; // 44
  const ADDR_LASER_DELAY = ADDR_CAM_EXPO+1; // 45
  
  const ADDR_AI = ADDR_LASER_DELAY+1;// 46

  const ADDR_VERSION = 200;
  const ADDR_ID = 201;
```

Since all the addresses follow each other and are dependent on the number of signals, the if-else conditions (lines 175 to 255) are valid in the current implementation. After changes, this might not be the case. Make sure there is no overlap between the different signal addresses, and that the fixed addresses (version and id) are not defined for one of the signals. Finally, compile the FPGA configuration and upload it to the FPGA (see [build the configuration](2_installing_microfpga.md) for a walkthrough).

Note that if you are using [Micro-Manager](using_micro-manager.md), the [Java](using_java.md) or the [Python](using_python.md) libraries, you will have to modify the addresses in the user code as well. The addresses are defined in a similar fashion in the following files:

- [Micro-Manager device adapter](https://github.com/mufpga/MicroFPGA-mm/blob/ec88b570e533122c0ce0223c18f39edf68f77a3a/MicroFPGA.cpp#L47): line 47 to 61.
- [Python library](https://github.com/mufpga/MicroFPGA-py/blob/2f455be3fdba87c680d4ca336b69d2ad7faa5268/microfpga/signals.py#L11): line 11 to 25.
- [Java library](https://github.com/mufpga/MicroFPGA-java/blob/766051054e9982a18474cf43dd8a4cfb13994a76/src/main/java/de/embl/rieslab/microfpga/devices/Signal.java#L13): line 13 to 27.

