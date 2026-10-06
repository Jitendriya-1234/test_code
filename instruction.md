# Project Guide

## Project Identity

- Workspace folder: `JCH2KOR_2`
- Eclipse project name: `rbd_cv_png_DTNA_IPDM_B_sw_dev_RWS_JCH2KOR_2`
- Project type: DTNA IPDM B embedded software project for an Infineon AURIX TC38x platform, using AUTOSAR Classic and Vector MICROSAR components.
- Active build variant: `rbd_starterkit_aurix2g_swbuild_Evalboard_TC38`

## Top-Level Folder Structure

| Path | Purpose |
| --- | --- |
| `rbd/png/proj/sw/` | Main project software, organized by AUTOSAR/application layer. |
| `rbd/png/bm/sw/` | Base-module software and shared application data. |
| `vector_png/Applications/` | Project-specific AUTOSAR configuration, application sources, generated data, and ECU inputs. |
| `vector_png/external/` | Vector MICROSAR components, DaVinci configurator content, documentation, and third-party components. |
| `infineon/` | Infineon device and platform materials, including user manuals. |
| `Tools/` | Build wrapper and Bosch MIC/CDG IDE configuration. |
| `_metadata/mic/` | Root MIC type, variant, and configuration metadata. |
| `_builds/` | Build-specific generated files, logs, metadata, and binary outputs. |
| `Instruction_md/` | Project instructions and developer notes. |

## Main Software Layers

The software under `rbd/png/proj/sw/` is grouped as follows:

| Folder | Purpose |
| --- | --- |
| `01_APP/` | Application software and wrappers, including Calibration DID, DCM, communication, main-switch, and safety components. |
| `02_RTE/` | Generated AUTOSAR Runtime Environment and ECU configuration. |
| `03_SL/` | Service-layer / basic software integration and generated configuration. |
| `04_ECUAL/` | ECU Abstraction Layer. |
| `05_MCAL/` | Microcontroller Abstraction Layer and device drivers. |
| `06_CDD/` | Complex Device Drivers and safety-related modules. |
| `07_LIB/` | Libraries. |
| `08_common/` | Shared software, utilities, and common configuration. |
| `architecture/` | Architecture-level project files. |
| `CICD/` | Continuous integration and delivery support files. |
| `featureData/`, `managementData/` | Feature and project management data. |
| `tools_cfg/` | Software build and tooling configuration. |

## Build Prerequisites

- Run the build on a Windows development environment with the Bosch CDG/CDGB toolchain installed and available through `tini`.
- The checked-in build wrapper initializes `cdg.de` and selects CDGB version `2019.2.0`.
- The active MIC build variant is `rbd_starterkit_aurix2g_swbuild_Evalboard_TC38`.
- Required compiler, linker, and licensed vendor tools must be available through the project’s configured development environment.

## Build Instructions

Open Command Prompt at the `JCH2KOR_2` project root, then run:

```bat
Tools\Build.bat rbd_starterkit_aurix2g_swbuild_Evalboard_TC38
```

`Tools\Build.bat` initializes the Bosch CDG environment, cleans the selected variant, and then builds it. The batch file accepts the variant as its first argument; use the active variant above unless the project configuration has been intentionally changed.

Build-specific output is written under:

```text
_builds/rbd_starterkit_aurix2g_swbuild_Evalboard_TC38/
```

This directory contains generated content under `_gen/`, logs under `_log/`, metadata under `_metadata/`, and binary output under `_bin/`.

## Build Configuration References

- Active variant selection: `_metadata/mic/temproot.mic`
- Variant definition: `_metadata/mic/tempvariants.mic`
- Build command implementation: `Tools/Build.bat`
- IDE MIC settings: `Tools/ide_properties.txt` and `Tools/ideConfiguration/`