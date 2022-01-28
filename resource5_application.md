# Application examples



In the Ries lab, several microscopes are equipped with MicroFPGA together with [Micro-Manager](https://micro-manager.org/) and [htSMLM](https://github.com/jdeschamps/htSMLM). In this section, we detail some aspect of our usage.



## Tested devices

|       Signal        |   Electronics   |                            Device                            |       Use       |
| :-----------------: | :-------------: | :----------------------------------------------------------: | :-------------: |
| Camera trigger (in) |      None       |                  Hamamatsu ORCA-Flash4.0 V2                  |     Trigger     |
| Camera trigger (in) |  SCB 5V->3.3V   |      Photometrics Evolve 512<br />Andor iXon Ultra 897       |     Trigger     |
| Laser trigger (out) |      None       | Toptica iChrome MLE <br />Toptica iBeamSmart<br />Omicron LightHUB<br />Custom [LaserEngine](https://github.com/ries-lab/LaserEngine) |     Trigger     |
|     Servo (out)     |      None       | Sail winch servos (e.g.: [1](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Filter_wheel), [2](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Flip_mount) and [3](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Linear_stage)) |  Move elements  |
|      PWM (out)      |      None       | Custom [LaserEngine](https://github.com/ries-lab/LaserEngine) |   Laser power   |
|      PWM (out)      | SCB PWM->Analog |                             AOM                              |   Laser power   |
|      TTL (out)      |      None       |        Owis KSHM 40<br />Custom bright-field LED ring        | In/Out, On/Off  |
|     Analog (in)     |    ACB -> 1V    | Custom [focus-stabilization](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Focus-locking)<br />Custom [laser power meter](https://github.com/ries-lab/RiesPieces/tree/master/Electronics/Powermeter) | Reading signals |

SCB: signal conversion board (see [electronics](electronics.md))

ACB: analog conversion board (see [electronics](electronics.md))



## GUI

Our microscopes are controlled through [Micro-Manager](https://micro-manager.org/) and a custom [EMU](https://github.com/jdeschamps/EMU) plugin: [htSMLM](https://github.com/jdeschamps/htSMLM). Here is an overview of the mapping of the FPGA signals (device properties) in Micro-Manager to the htSMLM functionalities. Refer to the [htSMLM guide](https://github.com/jdeschamps/htSMLM/tree/master/guide) for more details, in particular the [descriptions](https://github.com/jdeschamps/htSMLM/blob/master/guide/using-htsmlm.md) of each panel.

|                       Signal                        |                        htSMLM panels                         |
| :-------------------------------------------------: | :----------------------------------------------------------: |
| Laser trigger<br />(mode, pulse duration, sequence) | Laser trigger panels<br />Activation laser panel<br />Activation script panel |
|                        Servo                        | Filters panel<br />Additional filters panel<br />Controls panel |
|                         PWM                         |                     Laser control panels                     |
|                         TTL                         |                        Controls panel                        |
|                       Analog                        |               QPD panel<br />Powermeter panel                |

Together, the GUI and MicroFPGA allows intuitive control of the microscope and automated localization microscopy.



## Publications

MicroFPGA earlier versions have been used in the following publications (non-exhaustive list) and in most Ries lab (EMBL) projects:

#### Instrumentation

- Deschamps, Joran, Andreas Rowald, and Jonas Ries. "Efficient homogeneous illumination and optical sectioning for quantitative single-molecule  localization microscopy." *Optics express* 24.24 (2016): 28080-28090. [link](https://opg.optica.org/oe/abstract.cfm?uri=oe-24-24-28080)
- Schröder\*, Daniel, Deschamps\*, Joran  et al. "Cost-efficient open source laser engine for microscopy." *Biomedical optics express* 11.2 (2020): 609-623. [link](https://opg.optica.org/boe/fulltext.cfm?uri=boe-11-2-609&id=425622)
- Dasgupta\*, Anindita, Deschamps\*, Joran et al. "Direct supercritical angle localization microscopy for nanometer 3D superresolution." *Nature communications* 12.1 (2021): 1-9. [link](https://www.nature.com/articles/s41467-021-21333-x)

#### Biology

- Mund, Markus, et al. "Superresolution microscopy reveals partial  preassembly and subsequent bending of the clathrin coat during  endocytosis." *bioRxiv* (2021). [link](https://www.biorxiv.org/content/10.1101/2021.10.12.463947v2.abstract)
- Thevathasan, Jervis Vermal, et al.  "Nuclear pores as versatile reference standards for quantitative  superresolution microscopy." *Nature methods* 16.10 (2019): 1045-1053. [link](https://www.nature.com/articles/s41592-019-0574-9)
- Mund, Markus, et al. "Systematic nanoscale analysis of endocytosis links efficient vesicle formation to patterned actin nucleation." *Cell* 174.4 (2018): 884-896. [link](https://www.sciencedirect.com/science/article/pii/S0092867418308006)