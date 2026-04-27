.. _Release-note-label:

#############
Release Notes
#############

Overview
========

The **Processor Software Development Kit (Processor SDK)** is a unified software platform for TI embedded processors
providing easy setup and fast out-of-the-box access to benchmarks and demos.  All releases of Processor SDK are
consistent across TI’s broad portfolio, allowing developers to seamlessly reuse and develop software across devices.
Developing a scalable platform solutions has never been easier than with the Processor SDK and TI’s embedded processor
solutions.

To simplify the end user experience, Processor SDK Linux AM62A installer provides everything needed as discussed below
to create the embedded system from “scratch” :

-  Platform/board-support software and configuration files for Linux
-  U-Boot and Kernel sources and configuration files
-  An ARM cross-compiling toolchain as well as other host binaries and components
-  A Yocto/OE compliant filesystem and sources for example applications
-  A variety of scripts and Makefiles to automate certain tasks
-  Other components needed to build an embedded system that don’t fit neatly into one of the above buckets
-  Reference Examples, benchmarks

Licensing
=========

Please refer to the software manifests, which outlines the licensing
status for all packages included in this release. The manifest can be
found on the SDK download page or in the installed directory as indicated below.

-  Linux Manifest: :file:`<PSDK_PATH>/manifest/software_manifest.htm`


Release 11.02.11.03
===================

Released on Apr 2026

What's new
----------

**Processor SDK Linux AM62AX Release has following new features:**

  - Second 2025 LTS Reference Release Including RT combined branch model
  - In Vision AI SDK, CSIRX driver is now supported from FreeRTOS running on the DM-R5F core. As a result, CSIRX drivers are no longer supported in the Linux kernel.
  - EdgeAI memory carveouts now supported via `k3-am62a7-sk-edgeai.dtso <https://git.ti.com/cgit/ti-linux-kernel/ti-linux-kernel/tree/arch/arm64/boot/dts/ti/k3-am62a7-sk-edgeai.dtso?h=11.01.11>`_ in ti-linux-kernel & applied by default in the AM62A board environment via the name_overlays variable in ti-u-boot as seen in :file:`board/ti/am62ax/am62ax.env`
  - Linux EthFW client is now enabled via the :file:`k3-am62a7-sk-ethfw.dtbo` overlay
  - Important Bug Fixes on top of Processor SDK 11.01.07.05 Release

**Key Release References:**

  - RT Kernel : Real-Time Linux Interrupt Latency numbers here :ref:`RT Interrupt Latencies <RT-linux-performance>`
  - How standby power mode works - :ref:`CPUIdle Documentation <cpuidle-guide>`

**Component version:**

  - Kernel 6.12.57
  - U-Boot 2025.01
  - Toolchain GCC 13.4
  - ATF 2.13+
  - OPTEE 4.7.0+
  - TIFS Firmware / SYSFW `v11.02.10 <https://software-dl.ti.com/tisci/esd/11_02_10/release_notes/release_notes.html>`__ (Click on the link for more information)
  - DM Firmware MSDK.11.02.00.32
  - Yocto scarthgap 5.0
  
**Features no longer supported with Vision AI SDK:**

  - No support for Audio Codec (TLV320AIC3106) Linux driver
  - No support for V4L2 based CSI2RX
  - No support for EdgeAI Gstreamer Apps & QT based EdgeAI Gallery App
  - No support of V4L2 based Gstreamer pipelines for VPAC ISP & TIDL inferencing
  - No support for Custom TI Gstreamer plugins

.. _release-specific-build-information:

Build Information
=================

U-Boot
------

| Head Commit: f9285b5ec2ded0bd426a05599057715e52f6c520
| uBoot Version: 2025.01
| uBoot Tag: 11.02.11.03
|

TF-A
----
| Head Commit: e0c4d3903b382bf34f552af53e6d955fae5283ab
| Repo: https://git.trustedfirmware.org/plugins/gitiles/TF-A/trusted-firmware-a.git/
| Branch: master
| Tag: 2.13+
|

OP-TEE
------
| Head Commit: a9690ae39995af36a31b7a4f446f27ea0787e3a4
| Repo: https://github.com/OP-TEE/optee_os/
| Branch: master
| Tag: 4.7.0+
|

ti-linux-firmware
-----------------
| Head Commit: 51277d702acb8681ec38cc9a9979616d2f2c0ce9

Kernel
------
.. rubric:: Linux Kernel
   :name: linux-kernel

| Head Commit: de0910685fe405c575e83cf05351441498b13a34
| Kernel Version: v6.12.57
| use-kernel-config=defconfig
| non-rt-config-fragment=kernel/configs/ti_arm64_prune.config
|

.. _issue-tracker:

Issues Tracker
==============

.. note::

    - Release Specific Issues including details will be published through Software Incident Report (SIR) portal

    - Further Information can be found at `SIR Portal <https://sir.ext.ti.com/>`_

Errata Resolved
---------------
.. csv-table::
   :header: "Record ID", "Title"
   :widths: 15, 70

   "`EXT_EP-12128 <https://sir.ext.ti.com/jira/browse/EXT_EP-12128>`_","USB2 PHY locks up due to short suspend"
   "`EXT_EP-12123 <https://sir.ext.ti.com/jira/browse/EXT_EP-12123>`_","USART: Erroneous clear/trigger of timeout interrupt"
   "`EXT_EP-12124 <https://sir.ext.ti.com/jira/browse/EXT_EP-12124>`_","BCDMA: RX Channel can lockup in certain scenarios"
   "`EXT_EP-12114 <https://sir.ext.ti.com/jira/browse/EXT_EP-12114>`_","MMCSD: HS200 and SDR104 Command Timeout Window Too Small"

Issues Resolved
---------------
.. csv-table::
   :header: "Record ID", "Title"
   :widths: 15, 70

   "`EXT_EP-12785 <https://sir.ext.ti.com/jira/browse/EXT_EP-12785>`_","Cyclictest performance degradation on AM62x/AM64x/AM62A"
   "`EXT_EP-13147 <https://sir.ext.ti.com/jira/browse/EXT_EP-13147>`_","padconfig: ST_EN bit not preserved"
   "`EXT_EP-13169 <https://sir.ext.ti.com/jira/browse/EXT_EP-13169>`_","IPC: remoteproc fails to suspend/resume if there are no ipc firmwares in filesystem"
   "`EXT_EP-12226 <https://sir.ext.ti.com/jira/browse/EXT_EP-12226>`_","Linux SDK v10.0: U-Boot go command needs Linux Kernel-like cache/MMU cleanup so 3rd Party OS can startup correctly"
   "`EXT_EP-12970 <https://sir.ext.ti.com/jira/browse/EXT_EP-12970>`_","AM6x - Sitara Socs MCASP and BCDMA issue"
   "`EXT_EP-13312 <https://sir.ext.ti.com/jira/browse/EXT_EP-13312>`_","Wave5 Encoder Race condition leading to Kernel oops"
   "`EXT_SITMPUSW-154 <https://sir.ext.ti.com/jira/browse/EXT_SITMPUSW-154>`_","MSC ROI function not creating the desired ROI"
   "`EXT_EP-12747 <https://sir.ext.ti.com/jira/browse/EXT_EP-12747>`_","Codec: Wave5: Improve Decoder Performance and Fix SError Crash on Fluster test"
   "`EXT_EP-12787 <https://sir.ext.ti.com/jira/browse/EXT_EP-12787>`_","Multi channel decoding of h264 with high CPU load freezes on AM62A"

Issues Open
-----------
.. csv-table::
   :header: "Record ID", "Title"
   :widths: 15, 70

   "`EXT_SITMPUSW-76 <https://sir.ext.ti.com/jira/browse/EXT_SITMPUSW-76>`_","Heterogeneous-camera streaming has high latency while streaming imx390+ov2312"
   "`EXT_EP-12777 <https://sir.ext.ti.com/jira/browse/EXT_EP-12777>`_","OSPI XIP prefetch causes DMA transfer data corruption"
   "`EXT_SITMPUSW-151 <https://sir.ext.ti.com/jira/browse/EXT_SITMPUSW-154>`_","VPAC switching between WDR mode and linear mode causing wrong image color"
   "`EXT_EP-12043 <https://sir.ext.ti.com/jira/browse/EXT_EP-12043>`_","TPS6594: Error IRQ trap reach ilim, overcurrent for BUCK1/2 error"

