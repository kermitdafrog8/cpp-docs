---
title: "Troubleshoot Visual C++ Redistributable installation issues"
description: "Provide steps to diagnose and resolve issues with installing the Visual C++ Redistributable (VC Redist)"
author: vicroms
ms.author: viromer
ms.date: 02/04/2025
ms.topic: troubleshooting-general
helpviewer_keywords: [ "redist", "vcredist", "Visual [C++] redistributable", "VC Redist" ]
---
# Troubleshoot Visual C++ Redistributable installation issues

This guide is for users experiencing issues while installing the Visual C++
Runtime components using the Visual C++ Redistributable installer or the
Visual Studio Installer.

If you're experiencing such issues, we recommend that you first attempt
installing the [latest version of the Visual C++
Redistributable](latest-supported-vc-redist.md).

## Collect failure logs

The first step to diagnose an issue with the Visual C++
Redistributable (VC Redist) installer is to collect its failure logs.

1) Download the [Microsoft Visual Studio and .NET Log Collection
   Tool](<https://aka.ms/vscollect>).
2) Run `Collect.exe`
3) Extract the contents of `%TEMP%/vscollect.zip`

Once you extract `vscollect.zip`, the VC Redist logs are located inside the
`Temp` folder. The relevant log files are prefixed with the pattern
`dd_vcredist_<arch>_yyyyMMddHHmmss`.

In this article, we use these logs to diagnose common issues with the redist
installer.

### Other log locations

VC Redist is often executed as a prerequisite of other products, in such cases
the installation log might be found in a different path.

For example, [Configuration
Manager](/intune/configmgr/core/understand/introduction) upgrades VC Redist as
part of its own upgrade process, running `vcredist_x64.exe` with the `/l`
option, overriding the default log location.

In such cases, the path to the VC Redist logs can be found by reading that product's
own logs:

**Example: Configuration Manager logs**

`<ConfigMgr_Installation_Directory>\Logs\cmupdate.log`

```log
10-31-2025 17:40:06.421    CONFIGURATION_MANAGER_UPDATE    67368 (0x10728)    [Visual C++ 2015-2022 Redistributable (x64)] with older version 14.28.29914 is installed. it needs to upgraded.
10-31-2025 17:40:06.421    CONFIGURATION_MANAGER_UPDATE    67368 (0x10728)    INFO: Start install Visual C redistributable ("C:\Program Files\Microsoft Configuration Manager\CMUStaging\AA928926-5C76-4DE0-B51F-0FE4D365DFE2\SMSSETUP\BIN\X64\vcredist_x64.exe"  /q /norestart /l "C:\Program Files\Microsoft Configuration Manager\Logs\VCRedist64Install.log").
10-31-2025 17:40:14.553    CONFIGURATION_MANAGER_UPDATE    67368 (0x10728)    ERROR: Failed to install Visual C redistributable. Return code: 1603.
10-31-2025 17:40:14.553    CONFIGURATION_MANAGER_UPDATE    67368 (0x10728)    ERROR: 64-bit VC Redist installation ("C:\Program Files\Microsoft Configuration Manager\CMUStaging\AA928926-5C76-4DE0-B51F-0FE4D365DFE2\SMSSETUP\BIN\X64\vcredist_x64.exe") failed. Please check log file [C:\Program Files\Microsoft Configuration Manager\Logs\VCRedist64Install.log].
10-31-2025 17:40:14.554    CONFIGURATION_MANAGER_UPDATE    67368 (0x10728)    Failed to install vc redist. Please manually install it from C:\Program Files\Microsoft Configuration Manager\CMUStaging\AA928926-5C76-4DE0-B51F-0FE4D365DFE2\SMSSETUP\BIN\X64
```

## Return Code 1603

Issues with the VC Redist installer often produce the return code 1603. This is
a generic install failure code produced by the Windows Installer, which is
invoked during the installation of the Visual C++ Runtime components.

Because many factors can produce a 1603 code, the return code itself is not
enough to diagnose the root cause of the issue. In such cases, the log files
usually contain relevant information that can lead to a solution.

The [Common issues](#common-issues) section describes examples of how to
diagnose common installation errors and steps that may resolve them. If your
issue is not found here, then follow the instructions to [report an issue in
the Visual C++ Redistributable installer](#my-issue-is-not-here).

## Common issues

### Error 1714 - Older Version Cannot Be Removed

Error 1714 is often caused by a corrupted Windows Installer Cache. The
installation process fails to remove an older version due to a corrupted
or missing MSI package.

**Diagnose**

> [!NOTE]
> The log file examples in this section have had the timestamps removed to
> present only the relevant information.

> [!NOTE]
> The GUIDs on this examples may be different depending on the product version
> being installed.

The presence of these error messages indicate a corrupted cache.

In `dd_vcredist_<arch>_<timestamp>.log`

```log
Error 0x80070003: Failed to get size of pseudo bundle: C:\ProgramData\Package Cache\{43d1ce82-6f55-4860-a938-20e5deb28b98}\VC_redist.x64.exe
Error 0x80070003: Failed to initialize package from related bundle id: {43d1ce82-6f55-4860-a938-20e5deb28b98}
```

In  `dd_vcredist_<arch>_<timestamp>_vcRuntimeMinimum_<arch>.log`:

```log
SOURCEMGMT: Trying source C:\ProgramData\Package Cache\{455DF12C-7D43-4EFF-AE2F-43C8AF2817A3}v14.28.29914\packages\vcRuntimeMinimum_amd64\.
Note: 1: 2203 2: C:\ProgramData\Package Cache\{455DF12C-7D43-4EFF-AE2F-43C8AF2817A3}v14.28.29914\packages\vcRuntimeMinimum_amd64\vc_runtimeMinimum_x64.msi 3: -2147287037 
SOURCEMGMT: Source is invalid due to missing/inaccessible package.
```

```log
Note: 1: 1714 2: Microsoft Visual C++ 2022 X64 Minimum Runtime - 14.40.33816 3: 1612 
CustomAction  returned actual error code 1612 (note this may not be 100% accurate if translation happened inside sandbox)
Product: Microsoft Visual C++ 2022 X64 Minimum Runtime - 14.40.33816 -- Error 1714. The older version of Microsoft Visual C++ 2022 X64 Minimum Runtime - 14.40.33816 cannot be removed.  Contact your technical support group.  System Error 1612.

Error 1714. The older version of Microsoft Visual C++ 2022 X64 Minimum Runtime - 14.40.33816 cannot be removed.  Contact your technical support group.  System Error 1612.
```

In `VSSetupEvents.txt`

```log
Error 1714. The older version of Microsoft Visual C++ 2022 X64 Minimum Runtime - 14.40.33816 cannot be removed.  Contact your technical support group.  System Error 1612.] [(NULL)] [(NULL)] [(NULL)] [(NULL)] [(NULL)] []
```

**Steps to resolve**

From the log files, take note of the VC Redist version causing the issue.

Method 1: Use the Windows Installer:

1. Try using the Windows Installer to manually remove the old VC Redist version.
   If prompted, let the Windows Installer Troubleshooter attempt to fix the
   issue.
2. Retry the installation.

Method 2: Manually remove the old version.

1. Download the VC Redist installer for the old version by following the steps in
   [Download old versions of the Visual C++ Redistributable Installer](#old-vcredist-versions)
2. Run the installer to uninstall the old VC Redist.
3. Retry the installation.

## <a name="old-vcredist-versions"></a> Download old versions of the Visual C++ Redistributable Installer

> [!WARNING]
> Never install a Visual C++ Redistributable Installer that wasn't downloaded
> from a Microsoft site. And only install packages that are signed by Microsoft.

The VC Redist installer can be downloaded from
[my.visualstudio.com](<https://my.visualstudio.com/Downloads>), search for
Visual C++ Redistributable

The latest supported VC Redist version for each version of Visual Studio can
be found in [this article](/cpp/windows/latest-supported-vc-redist).

To access older or legacy versions follow these steps:

**Version 14.50 or later**

The download links use the
`https://aka.ms/vs/18/release/<version>/VC_redist.<arch>.exe` pattern.
For example: <https://aka.ms/vs/18/release/14.50.35719/VC_redist.x64.exe>.

**Version 14.30 to 14.44**

The download links use the
`https://aka.ms/vs/17/release/<version>/VC_redist<arch>.exe` pattern.
For example: <https://aka.ms/vs/17/release/14.32.31332/VC_redist.arm64.exe>.

**Version 14.20 to 14.29**

The download links use the
`https://aka.ms/vs/16/release/<version>/VC_redist<arch>.exe` pattern.
For example: <https://aka.ms/vs/16/release/14.28.29914/VC_Redist.x86.exe>

**Version 14.10 or later**

The download links use the
`https://aka.ms/vs/15/release/<version>/VC_redist<arch>.exe` pattern.
For example: <https://aka.ms/vs/15/release/14.12.25810/VC_redist.x64.exe>

If the aka.ms links do not work, you may be able to find the version you're
looking for through a Bing search. However, make sure that the download
comes from a Microsoft site and that the installer is signed by Microsoft.

## My issue is not here

TBD: Instructions to report an issue with the redist installer.
