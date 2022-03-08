# Electronics

In order to use MicroFPGA with downstream devices, voltage conversion is sometimes necessary. Indeed, Alchitry FPGAs present the following limitations:

- Output voltages are limited to 3.3 V.
- Digital inputs must be smaller than 3.3 V.
- No analog output signals natively.
- Analog input voltages are measured up to 1 V and must be smaller than 1.8 V (Au/Au+ FPGA). **If higher voltages are supplied, the FPGA can be irreversibly damaged.**

Here, we provide two custom electronic boards to convert voltages to acceptable levels for the FPGA or downstream devices:

- [Signal conversion board](https://github.com/mufpga/MicroFPGA-electronics/Signal_conversion_board): multi-channel electronics allowing conversion of 3.3 V signals to 5 V, or inversely, with the option to low-pass the input signal in order to produce an analog signal output from a PWM (pulse-width modulation) input.
- [Analog conversion board](https://github.com/mufpga/MicroFPGA-electronics/Analog_conversion_board): multi-channel electronics converting 10 V or 5 V analog signals to 1 V, with the option to cap the maximum voltage to 1.6 V.

## Signal conversion board

<img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Signal_conversion_board/SCB.jpg" alt="SCB" width="100"/>

#### Channels

The [signal conversion board](https://github.com/mufpga/MicroFPGA-electronics/Signal_conversion_board) is composed of 8 channels:

- 4 voltage conversion channels with optional low-pass filter.
- 4 bidirectional voltage conversion channels.

The channels only differ by the analog detour option. For the conversion channels without analog detour, or when the analog detour is ignored, the channels can be used in either direction: voltage A -> voltage B or B ->  A. **When the analog detour is soldered in, the voltage conversion is only performed A -> B**. The low pass step is performed by a Sallen-Key circuit with a cut-off at 10 Hz. 

In order to choose the input and output voltages, refer to the channel header:

![Signal conversion board](https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Signal_conversion_board/SCB_channel.jpg)

The channel header allows choosing the following parameters:

- **Voltage A**: 3.3 V, 4 V or 5 V. **A single voltage** must be chosen by soldering the two pads together.
- **Direction**: solder either "<---" or "--->" to choose the conversion direction between voltages A and B. **If you are using the analog detour, choose "--->".**
- **Voltage B**:  3.3 V, 4 V or 5 V. **A single voltage** must be chosen by soldering the two pads together.
- **Analog detour**: the analog detour is a low-pass RC filter that takes a **PWM** signal in input and output an **analog** signal. **In order to use the analog detour, select the "A --> B" direction.**

#### Power supply

The board is powered by a 5 V power supply (1 A). We typically use the same external power supply for the FPGA and the signal conversion board.

#### Folder content

The [signal conversion board folder](https://github.com/mufpga/MicroFPGA-electronics/Signal_conversion_board) contains the following subfolders:

- Altium project: complete project generated with Altium 17.1.9 (Build 592).
- BOM: bill of materials exported from the Altium project.
- Circuit: summary pdf containing an overview of the boards and the different circuits, generated from the Altium project.
- Gerber: gerber layers compatible with [gerbv](http://gerbv.sourceforge.net/), generated from the Altium project.
- NC drill: numeric control drill files corresponding to the PCB board, generated from the Altium project.

#### Use cases

- ##### Example 1: EMCCD camera with a 5 V laser trigger signal.

  In order to supply a 3.3 V camera trigger to the FPGA, one channel from the signal conversion board can be used. First, select the direction by soldering the "--->" or "<---" path. Then, solder in the arrow's input the 5 V level, and in the arrow's output the 3.3 V level. If the channel contains an analog detour option, solder the "no" path. 

- ##### Example 2: device with a 5V analog control signal.

  Using a PWM channel from the FPGA as input A to one channel, we can create an analog output between 0-5 V by setting the A voltage to 3.3 V, the "--->" direction, voltage B as 5 V and soldering both "yes" pads on the analog detour. While the PWM signal is a digital signal with pulses between 1 and 2 ms, the output analog signal will have a voltage directly dependent on the PWM pulse length.



## Analog conversion board

<img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Analog_conversion_board/ACB.jpg" alt="ACB" width="100"/>

#### Channels

Since the Au FPGA analog input are limited to the 0-1 V range and are only safe up to 1.6 V, an additional circuit is necessary to convert commonly encountered 5 and 10 V inputs. The [analog conversion board](https://github.com/mufpga/MicroFPGA-electronics/Analog_conversion_board) is composed of 8 channels allowing 1/10 or 1/5 voltage conversion. Additionally, the voltage and current limit can be disabled.

![Signal conversion board](https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Analog_conversion_board/ACB_channel.jpg)

Each channel header present options that need to be jumped:

- **Division**: 1/10 or 1/5. One of the two division level must be chosen. 
- **Output limitation**: 
  - Jumper on the **voltage and current limit**: the output voltage and current will be caped in order to prevent damages to the FPGA.
  - Jumper on the **limitation off**: the output voltages and current will not be caped. **This may endanger your FPGA.**
  - No jumper: only the output current is capped.

#### Power supply

The board is powered by a 12 V power supply (1 A).

#### Folder content

The [analog conversion board](https://github.com/mufpga/MicroFPGA-electronics/Analog_conversion_board) contains the following subfolders:

- Altium project: complete project generated with Altium 17.1.9 (Build 592).
- BOM: bill of materials exported from the Altium project.
- Circuit: summary pdf containing an overview of the boards and the different circuits, generated from the Altium project.
- Gerber: gerber layers compatible with [gerbv](http://gerbv.sourceforge.net/), generated from the Altium project.
- NC drill: numeric control drill files corresponding to the PCB board, generated from the Altium project.

#### Use case

If a sensor on the microscope has an analog output comprised between 0 and 10 V, feeding it directly to the Au FPGA will saturate the read-out channel. Therefore, the signal is set as input of the conversion board, with the 1/10 option selected as well as the "voltage and current limitation" one. The output of the channel is then safe to be wired to the FPGA and the will allow reading out the signal.

Examples of applications are for instance monitoring the [laser power meters](https://github.com/ries-lab/RiesPieces/tree/master/Electronics/Powermeter) or the [focus of the microscope](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Focus-locking). 

## Electronic box

The FPGA and the complementary boxes can be assembled into a complete box:

<img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/Box.jpg" alt="Boards overview" width="700"/>

This particular example for the Au FPGA can be found in the [MicroFPGA electronics repository](https://github.com/mufpga/MicroFPGA-electronics).

### Step-by-step

In this section, we describe a rough step-by-step building of the FPGA box.  

1. The box is 3D printed and contains an Au FPGA and a Br shield (Alchitry), a custom [FPGA shield](https://github.com/mufpga/MicroFPGA-electronics/tree/main/FPGA_shield), an [analog conversion board](https://github.com/mufpga/MicroFPGA-electronics/Analog_conversion_board), a  [signal conversion board](https://github.com/mufpga/MicroFPGA-electronics/Signal_conversion_board) and three panels ([1](https://github.com/mufpga/MicroFPGA-electronics/tree/main/Box_panel_1), [2](https://github.com/mufpga/MicroFPGA-electronics/tree/main/Box_panel_2) and [3](https://github.com/mufpga/MicroFPGA-electronics/tree/main/Box_panel_3)). The bill of materials for each custom board can be found in their respective folders. Additional parts list can be found [in the Box subfolder](https://github.com/mufpga/MicroFPGA-electronics/tree/main/Box). 
   <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/1_boards.jpg" alt="Boards overview" width="600"/>
2. The Br shield is mounted on top of the Au FPGA and secured using the metal spacing bolts (see previous picture).
3. The FPGA shield will be mounted directly on top of the Br shield. The FPGA shield features connectors that ensure robust connection without possibility to invert GND and signal.
   <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/2_shield.jpg" alt="FPGA shield" width="600"/>
4. The jumpers are placed on the ACB channels to set the voltage conversion, for instance 0-10V to 0-1V with voltage and current limitation:
   <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/3_ACB_jumpers.jpg" alt="ACB jumpers" width="600"/>
5. The SCB does not feature jumpers but solder bridges instead. For each channel, the relevant bridges are therefore soldered, for instance 5V to 3.3V left to right:
   <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/4_SCB_path_soldering.jpg" alt="SCB solder bridges" width="600"/>
6. All panels and boards are then screwed on the 3D printed box (here without the FPGA shield).
   <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/5_assembled_box.jpg" alt="Assembled box" width="600"/>
7. Then, mount the FPGA shield:
8. <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/6_mounted_shield.jpg" alt="FPGA shield" width="600"/>
9. In order to connect the different boards, we used pre-made cables. The GND is not always used, as a single GND-GND connection between two boards is sufficient while any other GND-GND connection is redundant. This simplifies the cabling, preventing it from becoming too crowded.
   <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/7_cable_bundles.jpg" alt="Cables" width="300"/>
10. We then connect the boards to the power sources of [panel 3](https://github.com/mufpga/MicroFPGA-electronics/tree/main/Box_panel_3). At the time of the first connection, we recommend using a lab power supply that shows current and offers current protection. This allows powering each board step by step and watching the current consumption. Current consumption increasing significantly can be a sing of a soldering problem somewhere in the boards.
    <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/8_power_supply.jpg" alt="Power supplies" width="800"/>
11. We use the cables to wire the [second panel](https://github.com/mufpga/MicroFPGA-electronics/tree/main/Box_panel_2) to the ACB and the FPGA shield.
    <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/9_panel2_connection.jpg" alt="Panel 2 connection" width="800"/>
12. And the [first panel](https://github.com/mufpga/MicroFPGA-electronics/tree/main/Box_panel_1) to the SCB channels and the FPGA shield.
    <img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/10_panel1_connection.jpg" alt="Panel 1 connection" width="800"/>
13. Finally, we mount a heat sink on top of panel 3. The final box looks as follows:

<img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/11_final.jpg" alt="Final result" width="600"/>

<img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/12_final.jpg" alt="Final result" width="600"/>

<img src="https://raw.githubusercontent.com/mufpga/MicroFPGA-electronics/main/Box/step_by_step/13_final.jpg" alt="Final result" width="600"/>

All custom electronic boards and side panels were designed by Christian Kieser (Electronic workshop, EMBL). 
