### Analog read-out

Analog signals are often used to measure the state of the microscope in parallel to an experiment. For instance, [laser power meters](https://github.com/ries-lab/RiesPieces/tree/master/Electronics/Powermeter) allow monitoring the real-time laser power on the microscope by generating an analog signal. Likewise, they can be used to maintain the [focus of the microscope](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Focus-locking), while being measured on a computer for visual feedback.

MicroFPGA has eight analog read-out pins. Using the Au\Au+ FPGA, you can read-out the measured voltage scaled to 0-65535 on each channel. The FPGA uses Zynq-7000 SoC XADC Dual 12-Bit 1 MSPS Analog-to-Digital Converter from Xilinx. **The analog inputs are only available with the Au/Au+ FPGA.**

|        Properties         |         |
| :-----------------------: | :-----: |
|    Number of channels     |    8    |
|        Input range        |  0-1 V  |
| Maximum voltage tolerance |  1.8 V  |
|       Output range        | 0-65535 |

**The ADC can be damaged if the voltage input is higher than 1.8 V**, make sure to restrain the voltage within the 0-1 V range. The [ACB board](resource1_electronics.md) allows scaling analog voltages from 0-10 V or 0-5 V to 0-1 V, while also limiting the maximum voltage to 1.6 V. We therefore advise using such a board with MicroFPGA.

