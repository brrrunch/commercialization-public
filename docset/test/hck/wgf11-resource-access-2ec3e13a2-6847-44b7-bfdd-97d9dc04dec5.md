---
author: joshbax-msft
title: WGF11 Resource Access 2
description: WGF11 Resource Access 2
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: cb56a398-1150-4c3c-b93e-0b70a0394fae
---

# WGF11 Resource Access 2


This automated test verifies D3D graphics driver/hardware conformance for resource copying functions and the integrity of the data manipulated. There are also groups for D3D10.1 features that allow copying of compressed textures to structured formats and copying of multisample resources.

This topic applies to the following test jobs:

-   WGF11 Resource Access

-   WGF11 Resource Access (WoW64)

-   WGF11 Resource Access FL9.3

-   WGF11 Resource Access FL9.3 (WoW64)

## Test details


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Associated requirements</strong></p></td>
<td><p>Device.Graphics.AdapterRender.D3D101Core.D3D101CorePrimary Device.Graphics.AdapterRender.D3D101WDDM12.D3D101v12Primary Device.Graphics.AdapterRender.D3D10Core.D3D10CorePrimary Device.Graphics.AdapterRender.D3D10WDDM12.D3D10v12Primary Device.Graphics.AdapterRender.D3D111Core.D3D111CorePrimary Device.Graphics.AdapterRender.D3D11Core.D3D11CorePrimary Device.Graphics.AdapterRender.D3D11WDDM12.D3D11v12Primary</p>
<p>[See the device hardware requirements.](http://go.microsoft.com/fwlink/p/?linkid=254483)</p></td>
</tr>
<tr class="even">
<td><p><strong>Platforms</strong></p></td>
<td><p>Windows 7 (x64) Windows 7 (x86) Windows RT (ARM-based) Windows 8 (x64) Windows 8 (x86) Windows Server 2012 (x64) Windows Server 2008 R2 (x64) Windows RT 8.1 Windows 8.1 x64 Windows 8.1 x86 Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p><strong>Expected run time</strong></p></td>
<td><p>~20 minutes</p></td>
</tr>
<tr class="even">
<td><p><strong>Categories</strong></p></td>
<td><p>Certification Functional</p></td>
</tr>
<tr class="odd">
<td><p><strong>Type</strong></p></td>
<td><p>Automated</p></td>
</tr>
</tbody>
</table>

 

## Running the test


Before you run the test, complete the test setup as described in the test requirements: [Graphic Adapter or Chipset Testing Prerequisites](graphic-adapter-or-chipset-testing-prerequisites.md).

## Troubleshooting


For troubleshooting information, see [Troubleshooting Device.Graphics Testing](troubleshooting-devicegraphics-testing.md).

All test cases return PASS or FAIL. Review the test results in the log file for specific details about failures. The test might return SKIP if a format is not supported by the device, or if the feature level is lower than the one required to test a particular feature (10.1 for CopyMultisample/CopyCompressed). The test might return BLOCKED if there is an uncaught exception (framework catches it at the end and logs it). To review test details, review the test log from the DTM Studio.

## More information


You can access and modify the contents of resources through four functions: CopyResource(), CopySubresourceRegion(), UpdateSubresource(), and Map().

-   Test behavior when specifying regions that are 1 pixel in size and other special cases.

-   Ensure consistent data when copying from mip (progressively smaller and less detailed versions of the texture) and array slices.

-   Make sure that only specified data is changed and other subresources or regions remain untouched.

-   Test behavior with special and compressed formats.

-   Watch for CopyResource() and related functions that affect pipeline statistics. You can choose to use the rendering pipeline to "emulate" copy functionality, but the specification states that copy functions cannot affect pipeline statistics.

**CopyMultisample**

Tests support for the D3D10.1 feature of copy multisample resources.

-   Varies the number of samples used.

-   Ensures a unique value in each sample location.

-   Verifies that this is preserved on copy on the destination resource.

**CopyCompressed**

Verifies support for copying of compressed textures to structured formats which was added in D3D10.1. The compatible structured format (i.e. traditional 3-4 color channels) for each compressed texture is tested to make sure the data in the original texture is preserved on copy. No conversion should take place. This is a bit-for-bit copy. Roundtrip copy (structured-&gt;compressed) is also tested and should also be bit-for-bit accurate.

### Command syntax

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Command option</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Wgf11resourceaccess</strong></p></td>
<td><p>Runs the test jobs. Without any options, the test enumerates devices.</p></td>
</tr>
<tr class="even">
<td><p><strong>-FeatureLevel:XX.X</strong></p></td>
<td><p>Sets the feature level, where XX.X is the Feature Level the test will run at: 10.0, 10.1, or 11.0.</p></td>
</tr>
</tbody>
</table>

 

**Note**  
For command line help for this test binary, type **/?**.

 

### File list

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>File</th>
<th>Location</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Configdisplay.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\tools\</p></td>
</tr>
<tr class="even">
<td><p>D3d11_1sdklayers.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\graphics\d3d\support\</p></td>
</tr>
<tr class="odd">
<td><p>D3d11ref.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\graphics\d3d\support\</p></td>
</tr>
<tr class="even">
<td><p>D3d11sdklayers.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\graphics\d3d\support\</p></td>
</tr>
<tr class="odd">
<td><p>D3dcompiler_test.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\graphics\d3d\support</p></td>
</tr>
<tr class="even">
<td><p>D3dx10_test.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\graphics\d3d\support\</p></td>
</tr>
<tr class="odd">
<td><p>d3dx11_test.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\graphics\d3d\support\</p></td>
</tr>
<tr class="even">
<td><p>TDRWatch.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\graphics\</p></td>
</tr>
<tr class="odd">
<td><p>Wgf11resourceaccess.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\graphics\d3d\conf</p></td>
</tr>
</tbody>
</table>

 

 

 





