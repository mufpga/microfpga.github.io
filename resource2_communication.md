# Register interface

The communication interface is based on the [Register interface for the Mojo](https://alchitry.com/register-interface-mojo) from Alchitry. 



Each parameter in MicroFPGA has an address used for reading/writing its value that depends also on the channel of the signal it corresponds to (e.g. the id of the laser). MicroFPGA has the following parameters for the Au/Au+ (i.e. with analog read-out), with 1 camera (fixed), 8 lasers, 4 TTL, 7 servomotors, 5 PWM and 8 analog inputs (fixed):

|            Signal             |     Parameter     |       Address        |    Range     |
| :---------------------------: | :---------------: | :------------------: | :----------: |
|         Laser trigger         |       mode        |    Laser id (0-7)    |     0-4      |
|         Laser trigger         |     duration      |  8 + Laser id (0-7)  |   0-65535    |
|         Laser trigger         |     sequence      | 16 + Laser id (0-7)  |   0-65535    |
|              TTL              |       state       |  24 + TTL id (0-3)   |     0-1      |
|             Servo             |       state       | 28 + Servo id (0-6)  |   0-65535    |
|              PWM              |       state       |  35 + PWM id (0-4)   |    0-255     |
|        Camera trigger         |   trigger mode    |          40          |     0-1      |
|        Camera trigger         |    start/stop     |          41          |     0-1      |
|        Camera trigger         |       pulse       |          42          |   0-65535    |
|        Camera trigger         |      period       |          43          |   0-65535    |
|        Camera trigger         |     exposure      |          44          |   0-65535    |
|        Camera trigger         |       delay       |          45          |   0-65535    |
| Analog input<br />(read only) |       value       | 46 + Analog id (0-7) |   0-65535    |
|   Version<br />(read only)    | MicroFPGA version |         200          |      3       |
|      ID<br />(read only)      |     Board id      |         201          | 29, 79 or 80 |

The addresses are defined in the [top file of the Alchitry Labs project](https://github.com/mufpga/MicroFPGA/blob/main/Au/source/au_top.luc). A read request is answered by 4 bytes representing the queried value. Note that unknown addresses will cause the FPGA to answer **11206655** (error code).

Examples of the register interface implementations can be found here:

- **C++**: in the [Micro-Manager device adapter](https://github.com/jdeschamps/MicroFPGA/blob/master/Device_Adapter/MicroFPGA.cpp), line 308, 325 and 338.
- **Python**: in the [MicroFPGA-Py library](https://github.com/jdeschamps/MicroFPGA/blob/master/MicroFPGA-Py/microfpga/regint.py), line 39 and 57.
- **Java**: in the [MicroFPGA-Java library](https://github.com/jdeschamps/MicroFPGA/blob/master/MicroFPGA-Java/src/main/java/de/embl/rieslab/microfpga/regint/RegisterInterface.java), line 66 and 96.



