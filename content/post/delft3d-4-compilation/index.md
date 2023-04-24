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

## Download links

* Delft3D 4: [delft3d4/142586](https://svn.oss.deltares.nl/repos/delft3d/tags/delft3d4/142586/)
* Visual Studio Community 2019: [16.11](https://aka.ms/vs/16/release/vs_community.exe)
* Intel oneAPI Base Toolkit:
  * [2021.3](https://registrationcenter-download.intel.com/akdlm/irc_nas/17978/w_BaseKit_p_2021.3.0.3221.exe)
  * [2021.3 (offline installer)](https://registrationcenter-download.intel.com/akdlm/irc_nas/17978/w_BaseKit_p_2021.3.0.3221_offline.exe)
* Intel oneAPI HPC Toolkit:
  * [2021.3](https://registrationcenter-download.intel.com/akdlm/irc_nas/17940/w_HPCKit_p_2021.3.0.3227.exe)
  * [2021.3 (offline installer)](https://registrationcenter-download.intel.com/akdlm/irc_nas/17940/w_HPCKit_p_2021.3.0.3227_offline.exe)

Delft3D 4 compilation requires specific older versions (e.g., 2021). However, Intel's website only has download links for the latest version of the oneAPI toolkits. To get installers for older versions, Intel "suggests" its users to purchase a license from a reseller (see [this post](https://community.intel.com/t5/oneAPI-Registration-Download/How-to-download-Intel-compiler-2021-4/td-p/1365702)). In order to download older versions without purchasing a license, direct download links may be used. The following GitHub repository contains a list of download links for Intel oneAPI toolkits versions 2021.x and 2022.1:

* [github.com/hypersad/oneapi-release-history](https://github.com/hypersad/oneapi-release-history)

## Compilation

Compilation is straightforward thanks to the `build.bat` script:

* Open "Intel oneAPI command prompt for Intel 64 for Visual Studio 2019".
* Change working directory to the root source code folder (the one that contains `build.bat` and the `src` subfolder).
* Run `build.bat delft3d4` and wait for the automatic preparation and compilation.
* The compiled kernels will be in the `/build_delft3d4/x64` subfolder.
* This `x64` folder must be merged with the `x64` folder in the the GUI installation directory (replacing existing files) in order to use Delft3D from the graphical interface.
  * File `dioconfig.ini` in `\x64\dflow2d3d\default` must be copied to `\x64\dwaves\default` to run coupled wave-current models from the GUI.