# Micro-Manager

MicroFPGA device adapter is available directly from Micro-Manager.

1. Start Micro-Manager.
2. In the "Devices" menu, choose "Hardware Configuration Wizard...".
3. Create a new configuration or modify an existing one.
4. In the hardware list, find "MicroFPGA" and double click on the device adapter.
5. Select the relevant COMport and enter the baud-rate (**57600**). Click ok.
6. In the windows that opens, select the signals you want to use. Click next.
7. For each signal, select the number of channels. Click ok.
8. Save the new hardware configuration.
9. In the device property browser, available from the "Devices" menu, you have access to all properties from MicroFPGA.

> **Important**: The default baud-rate is **57600**. A wrong baud-rate will prevent
> communication with MicroFPGA.


# Java

The Java library is provided as a Maven project. In the following step we show how to import it in Eclipse:

1. If you don't have [git](https://git-scm.com/downloads), download and install it.

2. Using the newly installed git console, clone the MicroFPGA-java repository in the folder of your choice:

   ```bash
   $ cd /path/to/folder/
   $ git clone https://github.com/mufpga/MicroFPGA-java.git
   ```

3. Open Eclipse.

4. In the package explorer, import a new project. If the option is not available because projects already exist in your workspace, right-click and import a new project.

5. In the Maven folder, double-click on "Existing Maven Projects".

6. Click on "Browse" and navigate to the "MicroFPGA-Java" folder in the local git repository.

7. A "pom.xml" file should be automatically detected. Click on Finish.

8. After few seconds, Eclipse should automatically download the dependencies and set-up the project. The source folder containing the packages should be "src/main/java". If it is not the case, right-click on the project and select "Maven", then "Update Project".

9. The test folder (/src/main/test/) contains examples illustrating several aspects of MicroFPGA.

# Python

1. Install the serial and pyserial packages for Python (for instance using pip).

2. If you don't have [git](https://git-scm.com/downloads), download and install it.

3. Using the newly installed git console, clone the MicroFPGA-java repository in the folder of your choice:

   ```bash
   $ cd /path/to/folder/
   $ git clone https://github.com/mufpga/MicroFPGA-py.git
   ```

4. The examples folder contains scripts illustrating several aspects of MicroFPGA.

# Labview

A LabView example has been graciously provided by Christian Kieser (Electronic workshop, EMBL). It can be found in the MicroFPGA-LabView folder of the MicroFPGA repository. It is not supported in this repository and is only given as possible reference.
