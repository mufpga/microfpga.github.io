# Application examples



Several microscopes are equiped with MicroFPGA together with [Micro-Manager](https://micro-manager.org/) and [htSMLM](https://github.com/jdeschamps/htSMLM). In this section, we detail some aspect of our usage.



## Tested devices

|               Signal               |                            Device                            | Electronics |
| :--------------------------------: | :----------------------------------------------------------: | :---------: |
|            Camera (in)             |                   Photometrics Evolve 512                    |     SCB     |
|            Camera (in)             | Hamamatsu ORCA-Flash4.0 V2,<br />ORCA-Quest and ORCA-Fusion BT<br />PCO edge 4.2 and 4.2bi<br />Andor iXon Ultra 897 |    None     |
|            Camera (out)            |                  Hamamatsu ORCA-Flash4.0 V2                  |    None     |
|        Laser trigger (out)         | Toptica iChrome MLE and iBeamSmart<br />Omicron LightHUB<br />Oxxius LBX-405<br />Cobolt Jive 561<br />LaserQuantum gem 561<br />MPB Communications F-04306-107 and F-04-306-102 |    None     |
| Laser trigger (out)<br />PWM (out) | Custom laser engine ([link](https://github.com/ries-lab/LaserEngine)) |    None     |
|             TTL (out)              |                         LED switches                         |    None     |
|            Servo (out)             | Sail winch servos <br />(e.g.: [1](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Filter_wheel), [2](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Flip_mount) and [3](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Linear_stage)) |    None     |
| Analog (out):<br />PWM + low-pass  |     Omicron LH.AOM<br />AA Opto-Electronic AA.AOTF.6C/TN     |     SCB     |
|             TTL (out)              |                         Owis KSHM 40                         |    None     |
|            Analog (in)             | Focus stabilization ([link](https://github.com/ries-lab/RiesPieces/tree/master/Microscopy/Focus-locking))<br />Laser powermeter ([link](https://github.com/ries-lab/RiesPieces/tree/master/Electronics/Powermeter)) |     ACB     |

SCB: signal conversion board (see [electronics](resource1_electronics.md))

ACB: analog conversion board (see [electronics](resource1_electronics.md))



## Graphical user interface

The microscopes are controlled through [Micro-Manager](https://micro-manager.org/) and a custom [EMU](https://github.com/jdeschamps/EMU) plugin: [htSMLM](https://github.com/jdeschamps/htSMLM). Here is an overview of the mapping of the FPGA signals (device properties) in Micro-Manager to the htSMLM functionalities. Refer to the [htSMLM guide](https://github.com/jdeschamps/htSMLM/tree/master/guide) for more details, in particular the [descriptions](https://github.com/jdeschamps/htSMLM/blob/master/guide/using-htsmlm.md) of each panel.

|                       Signal                        |                        htSMLM panels                         |
| :-------------------------------------------------: | :----------------------------------------------------------: |
| Laser trigger<br />(mode, pulse duration, sequence) | Laser trigger panels<br />Activation laser panel<br />Activation script panel |
|                        Servo                        | Filters panel<br />Additional filters panel<br />Controls panel |
|                         PWM                         |                     Laser control panels                     |
|                         TTL                         |                        Controls panel                        |
|                       Analog                        |               QPD panel<br />Powermeter panel                |



## Publications

MicroFPGA earlier versions have been used in the following publications (non-exhaustive list) and in most Ries lab (EMBL) projects:

#### Instrumentation

- Deschamps, Joran, Andreas Rowald, and Jonas Ries. "Efficient homogeneous illumination and optical sectioning for quantitative single-molecule  localization microscopy." *Optics express* 24.24 (2016): 28080-28090. [link](https://opg.optica.org/oe/abstract.cfm?uri=oe-24-24-28080)
- Schröder\*, Daniel, Deschamps\*, Joran  et al. "Cost-efficient open source laser engine for microscopy." *Biomedical optics express* 11.2 (2020): 609-623. [link](https://opg.optica.org/boe/fulltext.cfm?uri=boe-11-2-609&id=425622)
- Dasgupta\*, Anindita, Deschamps\*, Joran et al. "Direct supercritical angle localization microscopy for nanometer 3D superresolution." *Nature communications* 12.1 (2021): 1-9. [link](https://www.nature.com/articles/s41467-021-21333-x)

#### Biology

- Mund, Markus, et al. "Superresolution microscopy reveals partial  preassembly and subsequent bending of the clathrin coat during  endocytosis." *bioRxiv* (2021). [link](https://www.biorxiv.org/content/10.1101/2021.10.12.463947v2.abstract)
- Diekmann, Robin, et al. "Optimizing imaging speed and excitation intensity for single-molecule localization microscopy." *Nature methods* 17.9 (2020): 909-912. [link](https://www.nature.com/articles/s41592-020-0918-5)
- Thevathasan, Jervis Vermal, et al.  "Nuclear pores as versatile reference standards for quantitative  superresolution microscopy." *Nature methods* 16.10 (2019): 1045-1053. [link](https://www.nature.com/articles/s41592-019-0574-9)
- Mund, Markus, et al. "Systematic nanoscale analysis of endocytosis links efficient vesicle formation to patterned actin nucleation." *Cell* 174.4 (2018): 884-896. [link](https://www.sciencedirect.com/science/article/pii/S0092867418308006)