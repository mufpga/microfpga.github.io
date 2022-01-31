# Changing the baud rate

The baud rate is a central parameter of serial communication and corresponds to the rate at which information is transferred between the computer and the FPGA. If the wrong baud rate is used for attempted communication, the communication will fail. The default baud rate of MicroFPGA is **57600**. 

### Changing the FPGA baud rate

In [au_top.luc](https://github.com/mufpga/MicroFPGA/blob/7908fc16b8069504b6fcd9e3213126e55c3c6d61/Au%2B/source/au_plus_top.luc#L106) (line 106 and 107), change the value "57600" to the relevant baud rate to your application (here for instance with 9600):

```verilog
uart_rx rx (#BAUD(9600), #CLK_FREQ(100000000)); // serial receiver
uart_tx tx (#BAUD(9600), #CLK_FREQ(100000000)); // serial transmitter
```

Compile the firmware and update the FPGA (see [Installing and building MicroFPGA](2_installing_microfpga.md) for a walkthrough).

### Changing the baud rate in the Java and Python libraries

In the Java [register interface](https://github.com/mufpga/MicroFPGA-java/blob/766051054e9982a18474cf43dd8a4cfb13994a76/src/main/java/de/embl/rieslab/microfpga/regint/RegisterInterface.java#L28) (line 28), change "57600" to "9600" (example baud rate):

```java
serialPort_.setComPortParameters(9600, 8, 1, 0);
```

In the Python [register interface](https://github.com/mufpga/MicroFPGA-py/blob/2f455be3fdba87c680d4ca336b69d2ad7faa5268/microfpga/regint.py#L10) (line 10), change "57600" to "9600" (example baud rate):

```python
if self._device is not None:
	self._serial = serial.Serial(self._device, 9600, timeout=1)
```

