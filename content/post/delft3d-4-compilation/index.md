---
title: Delft3D 4 Compilation
date: 2023-04-24T16:22:06.906Z
draft: false
featured: true
tags: []
image:
  filename: ""
  focal_point: Smart
  preview_only: false
---
*These instructions were adapted from [Mathew Topper
(H0R5E)](https://gist.github.com/H0R5E/162ffb929d946e9ccf1c9202e30c9b92).*

*I thank [Rafael Bueno](https://buenorc.github.io) for testing and providing valuable feedback.*

In order to compile Delft3D 4 kernels *tag 142586*, the following software is required:

1. *Visual Studio Community 2019* (version 16) with workload "Desktop development with C++" *and the following additional components:*

   * C++ MFC for latest v142 build tools (x86 & x64)
   * C++/CLI support for v142 build tools (Latest)
   * C++ Modules for v142 build tools (x64/x86 - experimental)
2. *Intel oneAPI Base Toolkit 2021*. To save disk space, I only install the following components:

   * Intel oneAPI Math Kernel Library
   * Intel Distribution for GDB
3. *Intel oneAPI HPC Toolkit 2021*. To save disk space, I only install the following components:

   * Intel MPI Library
   * Intel oneAPI DPC++/C++ Compiler & Intel C++ Compiler Classic
   * Intel Fortran Compiler (Beta) & Intel Fortran Compiler Classic

The components listed above do not guarantee a minimal installation (i.e., some of them may be unnecessary; feel free to test).

## Download links

* Delft3D 4 source code:
  * [Tag 142586](https://svn.oss.deltares.nl/repos/delft3d/tags/delft3d4/142586/) (use a Subversion client to export it)
* Visual Studio Community 2019:
  * [Instructions to install the Community edition using the Professional edition installer](https://stackoverflow.com/a/73593091)
  * [16.11.25 (Professional edition)](https://download.visualstudio.microsoft.com/download/pr/e0881e2b-53dd-47b3-a2c1-ba171c568981/9296c2a5f2a0f15019d24a788c8ddba08ebfca75a71076e4b14782ff11c55ab1/vs_Professional.exe)
* Intel oneAPI Base Toolkit:
  * [2021.3](https://registrationcenter-download.intel.com/akdlm/irc_nas/17978/w_BaseKit_p_2021.3.0.3221.exe)
  * [2021.3 (offline installer)](https://registrationcenter-download.intel.com/akdlm/irc_nas/17978/w_BaseKit_p_2021.3.0.3221_offline.exe)
* Intel oneAPI HPC Toolkit:
  * [2021.3](https://registrationcenter-download.intel.com/akdlm/irc_nas/17940/w_HPCKit_p_2021.3.0.3227.exe)
  * [2021.3 (offline installer)](https://registrationcenter-download.intel.com/akdlm/irc_nas/17940/w_HPCKit_p_2021.3.0.3227_offline.exe)

### Notes

Intel oneAPI 2021 toolkits are incompatible with Visual Studio Community 2019 version 16.11.**26** (released on April 11, 2023). Since the Community edition is only supported on the latest version (see [Product Lifecycle and Servicing](https://learn.microsoft.com/en-us/visualstudio/releases/2019/servicing-vs2019)), Microsoft does not provide Community edition installers for earlier versions (e.g., 16.11.**25**, which is compatible). However, it is still possible to install earlier versions of the Community edition using the installers of other editions (Professional, Enterprise or BuildTools). See [earlier Visual Studio 2019 releases](https://learn.microsoft.com/en-us/visualstudio/releases/2019/history) and [this Stack Overflow question](https://stackoverflow.com/questions/63297596/is-there-a-way-to-download-a-specific-version-of-visual-studio-2019).

T﻿he latest version of the Intel oneAPI 2021 toolkits is 2021.**4**. However, compilation of Delft3D 4 with 2021.**4** toolkits seems to be unsupported. Version 2021.**3** of the toolkits works without problems.

Delft3D 4 compilation requires Intel Fortran compiler version 2021, 2019, 2018 or 2016. However, on Intel's website you can only download the latest version (current year) of the oneAPI toolkits. To get installers for previous versions, Intel "suggests" its users to purchase a license from a reseller (see [this post](https://community.intel.com/t5/oneAPI-Registration-Download/How-to-download-Intel-compiler-2021-4/td-p/1365702)). In order to download older versions without purchasing a license, direct download links may be used. The following GitHub repository contains a list of download links for Intel oneAPI toolkits versions 2021.x and 2022.1: [github.com/hypersad/oneapi-release-history](https://github.com/hypersad/oneapi-release-history).

## Compilation

Compilation is straightforward thanks to the `build.bat` script:

* Open "Intel oneAPI command prompt for Intel 64 for Visual Studio 2019".
* Change the working directory using the `cd` command to the Delft3D source code folder (where `build.bat` is located).

  * Make sure that the path does not contain spaces. It is also advisable to use a short path (e.g., `C:\MyDelft3D\...`).
* Run `build.bat delft3d4` and wait for the automatic preparation and compilation.
* The compiled kernels will be in the `/build_delft3d4/x64` subfolder.
* This `x64` folder must be merged with the `x64` folder in the the GUI installation directory (replacing existing files) in order to use Delft3D from the graphical interface.

## Issues

* File `dioconfig.ini` in `\x64\dflow2d3d\default` must be copied to `\x64\dwaves\default` to run coupled wave-current models from the GUI.
* **I﻿f you find other installation issues, please let me know, and I will update the instructions.**