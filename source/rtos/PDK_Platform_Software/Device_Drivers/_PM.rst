.. http://processors.wiki.ti.com/index.php/Processor_SDK_RTOS_PM

Overview
--------

Introduction
^^^^^^^^^^^^

The Power Management (PM) low level driver provide power and thermal
management capabilities for RTOS applications.

.. rubric:: **Supported Devices**
   :name: supported-devices

+------------+---------+---------+--------+--------+----------+--------+--------+------------------------------+
| **Device** | **A53** | **A15** | **A8** | **A9** | **C66x** | **M4** | **R5F**| **Tested On**                |
+------------+---------+---------+--------+--------+----------+--------+--------+------------------------------+
| AM65xx     | X       |         |        |        |          |        | X      | AM65x EVM, AM65x IDK         |
+------------+---------+---------+--------+--------+----------+--------+--------+------------------------------+
| AM57xx     |         | X       |        |        | X        | X      |        | AM572x GP EVM, AM571x GP EVM |
+------------+---------+---------+--------+--------+----------+--------+--------+------------------------------+
| AM335x     |         |         | X      |        |          |        |        | AM335x GP EVM                |
+------------+---------+---------+--------+--------+----------+--------+--------+------------------------------+
| AM437x     |         |         |        | X      |          |        |        | AM437x GP EVM                |
+------------+---------+---------+--------+--------+----------+--------+--------+------------------------------+
| K2G        |         | X       |        |        | X        |        |        | K2G EVM                      |
+------------+---------+---------+--------+--------+----------+--------+--------+------------------------------+

.. note::

    PM on AM335x and AM437x devices supports only OPP modifications.  CPU idle
    and other PM modes on these devices are only for reference and are not
    validated on the EVM every release.

User Interface
--------------

Driver Configuration
^^^^^^^^^^^^^^^^^^^^^

.. rubric:: **Board Specific Configuration**
   :name: board-specific-configuration

The following board-specific actions must take place prior to calling
any PM Power APIs:

-  A board-specific I2C implementation must be registered with the PM
   HAL layer
-  The PMIC Ops structure matching the executing device's PMIC must be
   registered with PM HAL layer
-  Device clock rates must be initialized through the PM LIB layer

For working examples of how to implement the listed items, see the
"main" functions of any PM example in
``[PDK_INSTALL_DIR]\packages\ti\drv\pm\examples``.

.. rubric:: **PM Configuration Structure**
   :name: pm-configuration-structure

The pm\src\pmrtos\prcm\PowerDevice.c file configures the PM driver
through the PowerDevice_config structure. This structure must be
provided to PM driver. The structure is a global defined within
PowerDevice.c and must be initialized prior to calling Power_init(). The
structure cannot be changed after calling Power_init(). For details
about individual fields of this structure, see the Doxygen help by
opening
``[PDK_INSTALL_DIR]\packages\ti\drv\pm\docs\doxygen\html\index.html``.

APIs
^^^^^

The following lists the main application interfaces; see the end of this
page for a link to the API Reference Manual with full details.

PM TI RTOS base API reference for applications can be found in below
file:

::

    #include <ti/drv/pm/Power.h>  /* Contains the core TI RTOS Power implementation APIs */

PM TI RTOS extended API reference for applications can be found in the
below file:

::

    #include <ti/drv/pm/PowerExtended.h>  /* Contains TI RTOS Power API extensions such as thermal management */

PM TI RTOS device-specific API reference for applications can be found
in the below file:

::

    #include <ti/drv/pm/PowerDevice.h>  /* Contains device-specific TI RTOS Power API definitions and structures */

|

Application
------------

Examples
^^^^^^^

.. csv-table::
   :header: "Name", "Description", "Expected Results"
   :widths: 20, 30, 70

    "PM RTOS Application","Example demonstarting power management use cases. Reference example for developers","Application cycles the processor running the application through various power states using the PM APIs. User observes the output printed over the device's UART connection. **Note:** The example should be run in *Free Run* mode when loaded and executed in Code Composer Studio in order to prevent sleep API testing interruptions from the JTAG.  Use the following  steps to execute the application on the    AM57xx's M4 and C66 processors in Code Composer Studio:  -  Connect to CortexA15_0 waiting until the GEL file initialization completes -  Run the GEL: Scripts-->AM572x MULTICORE  Initialization-->AM572x_MULTICORE_EnableAllCores -  Connect to M4_IPU1_C0 or the C66xx_DSP1  -  Load the PM RTOS application's M4 or c66 executable -  Free run the M4_IPU1_C0 or the C66xx_DSP1"
    "PM RTOS Thermal Application","Example demonstrating thermal management use case. Reference example for developers","Application sets high and low thermal set points using the PM APIs.The set points are triggered by     internally heating up the processor.User observes the output printed over the device's UART connection. Use the following steps to execute the application on the AM57xx's M4 and C66 processors in Code Composer Studio:   -  Connect to CortexA15_0 waiting until the GEL file initialization completes -  Run the GEL:Scripts-->AM572x MULTICORE Initialization-->AM572x_MULTICORE_EnableAllCores -  Connect to M4_IPU1_C0 or the C66xx_DSP1 -     Load the PM RTOS Thermal application's M4 or c66 executable -  Run the M4_IPU1_C0 or the C66xx_DSP1"
    "PM Measurement Application ", "Menu-based application allowing selection of processor OPPs and benchmark tests.", "Application allows the user to control the processor's OPP settings via the PM driver. The application  also allows the user to select execution of the Dhrystone benchmark for performance and power profiling under different OPP settings. The application's menu is printed over the device's UART connection. **Note:** The     measurement application is only supported on the AM335x device at the moment."
    "PM System Configuration Test","Example demonstrating system configuration use-case", "This example is available at '<install_path>/packages /ti/drv/pm/examples/systemconfig'. The PM System Configuration test is an  example running on tda2xx A15 core, tda2xx M4 core,tda3xx IPU (M4) core and AM65xx(A53 and R5). This example demonstrates the ability to configure the desired power state for a given module based on the entries in the   power spread sheet.The example loops through the different modules and power states and tries to program the same for each module using PM LIB sysconfig APIs before declaring pass or fail.The example illustrates the   use of Power Management LIB which allows system configuration."
    "PM CLock Rate Configuration Test ","Example demonstrating clockrate configuration use-case","This example is available at '<install_path>/packages/ti/drv/pm/ examples/clkrate_manager' The Clock Rate Configuration test is an example running on A15 core and IPU (M4) Core for tda2xx/tda2ex/tda2px ,IPU (M4) core for tda3xx ,A53(MPU) and R5(MCU) for AM65xx. This example demonstrates the ability to read the clock rate for different clocks for a given CPU (MPU/IPU/DSP/GPU/IVA/EVE). The example first reads the current clock configuration and then checks for OPP_NOM, OPP_OD and OPP_HIGH frequencies along with voltage changes by using the PMLIB clock rate APIs before declaring pass or fail. The example illustrates the use of Power Management LIB which allows changing the CPU OPP. For AM65xx, this example first loops through all modules and gets the clockrate for all of their clocks.Then, it tries to set the frequencies for some clocks of different modules. "



Additional References
---------------------

+-----------------------------------+-----------------------------------------+
| **Document**                      | **Location**                            |
+-----------------------------------+-----------------------------------------+
| API Reference Manual              | $(TI_PDK_INSTALL_DIR)\\packages\\ti     |
|                                   | \\drv\\pm\\docs\\doxygen\\html\\index.h |
|                                   | tml                                     |
+-----------------------------------+-----------------------------------------+
| Release Notes                     | $(TI_PDK_INSTALL_DIR)\\packages\\ti     |
|                                   | \\drv\\pm\\docs\\ReleaseNotes_PM_LLD.   |
|                                   | pdf                                     |
+-----------------------------------+-----------------------------------------+

