# Register interface

The communication interface is based on the [Register interface for the Mojo](https://alchitry.com/register-interface-mojo) from Alchitry. The register interface allows reading/writing multiple times to the same address or to several consecutive addresses. MicroFPGA does not take advantage of this.

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

### Read example

In order to read the current value of a parameter, we send 5 bytes. The first byte is a read request (where the most significant bit is 0), while the other 4 are the address. For instance, to read the 4th laser (laser id = 3) duration (address = 8+3), we send the following request to the FPGA: 

|   Byte 0   |  Byte 1  |  Byte 2  |  Byte 3  |  Byte 4  |
| :--------: | :------: | :------: | :------: | :------: |
| read/write | address  | address  | address  | address  |
|  00000000  | 00001011 | 00000000 | 00000000 | 00000000 |

We then receive a 32 bits answer, with the least significant byte sent first. If the duration is 40 ms (value = 40'000, 1001110001000000 in binary), then the answer is the following:

|  Byte 0  |  Byte 1  |  Byte 2  |  Byte 3  |
| :------: | :------: | :------: | :------: |
|  value   |  value   |  value   |  value   |
| 01000000 | 10011100 | 00000000 | 00000000 |

### Write example

Following the previous example, in order to change the 4th laser duration to 55 ms (value = 55000, 1101011011011000 in binary), we should write:

|   Byte 0   |  Byte 1  |  Byte 2  |  Byte 3  |  Byte 4  |  Byte 5  |  Byte 6  |  Byte 7  |  Byte 8  |
| :--------: | :------: | :------: | :------: | :------: | :------: | :------: | :------: | :------: |
| read/write | address  | address  | address  | address  |  value   |  value   |  value   |  value   |
|  10000000  | 00001011 | 00000000 | 00000000 | 00000000 | 11011000 | 11010110 | 00000000 | 00000000 |

Where we see that the write request is indicated by the most significant bit in the first byte, and that the value is sent with the least significant byte first.

### Register interface implementations

Examples of the register interface implementations can be found here:

- **C++**: in the [Micro-Manager device adapter](https://github.com/mufpga/MicroFPGA-mm/blob/ec88b570e533122c0ce0223c18f39edf68f77a3a/MicroFPGA.cpp#L347), line 347 to 407.
- **Python**: in the [MicroFPGA-Py library](https://github.com/mufpga/MicroFPGA-py/blob/2f455be3fdba87c680d4ca336b69d2ad7faa5268/microfpga/regint.py#L42), line 42 to 81.
- **Java**: in the [MicroFPGA-Java library](https://github.com/mufpga/MicroFPGA-java/blob/766051054e9982a18474cf43dd8a4cfb13994a76/src/main/java/de/embl/rieslab/microfpga/regint/RegisterInterface.java#L39), line 39 to 76.



