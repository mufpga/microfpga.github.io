# MicroFPGA documentation

MicroFPGA is an FPGA-based platform for the electronic control of microscopes. It aims at using affordable FPGA to generate or read signals from a variety of devices, including cameras, lasers, servomotors, filter-wheels, etc. It can be controlled via [Micro-Manager](https://micro-manager.org/), or its Java, Python and LabView communication libraries, and comes with optional complementary [electronics](https://github.com/mufpga/MicroFPGA-electronics).

### Content

#### This repository contains the project Github pages, check out [mufpga.github.io](https://mufpga.github.io/).

### Related repositories

MicroFPGA is divided into multiple repositories:

- [FPGA configuration](https://github.com/mufpga/MicroFPGA)
- [Micro-Manager device adapter](https://github.com/mufpga/MicroFPGA-mm)
- [Java library](https://github.com/mufpga/MicroFPGA-java)
- [Python package](https://github.com/mufpga/MicroFPGA-py)
- [LabView library](https://github.com/mufpga/MicroFPGA-labview)
- [Complementary electronics](https://github.com/mufpga/MicroFPGA-electronics)

Additionally, MicroFPGA can be used together with other projects:

- [A Micro-Manager GUI](https://github.com/jdeschamps/htSMLM)
- [Ries lab repositories with compatible servomotor designs](https://github.com/ries-lab/RiesPieces)
- [A custom LaserEngine triggered by MicroFPGA](https://github.com/ries-lab/LaserEngine)


## Cite us
Joran Deschamps, Christian Kieser, Philipp Hoess, Takahiro Deguchi, Jonas Ries, "MicroFPGA: An affordable FPGA platform for microscope control",
HardwareX 2023 (13): e00407, doi:[10.1016/j.ohx.2023.e00407](https://doi.org/10.1016/j.ohx.2023.e00407).

### Contact

If you have any question, contact us via the [Image.sc](image.sc) forum (tag @jdeschamps or by PMs) or by email joran.deschamps[/at/]fht.org.

MicroFPGA and the Micro-Manager/Python/Java libraries were written by Joran Deschamps, EMBL (2020). The custom electronic boards and the LabView example were developed by Christian Kieser (Electronic Workshop, EMBL).
