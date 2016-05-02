---
author: joshbax-msft
title: Fibre Channel Adapter Testing Prerequisites
description: Fibre Channel Adapter Testing Prerequisites
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: e3465567-7afd-410e-91fc-2f2863c452a3
---

# Fibre Channel Adapter Testing Prerequisites


Tests for driver certification include manual and automated test cases. All automated and manual tests must pass for certification.

This section describes the tasks that you must complete before you test a Fibre Channel storage controller by using the Windows Hardware Certification Kit (Windows HCK):

-   [Review the hardware requirements](#bkmk-hardwarerequirements).

-   [Review the software requirements](#bkmk-softwarerequirements).

-   [Configure the test computer](#bkmk-configure).

## <a href="" id="bkmk-hardwarerequirements"></a>Hardware Requirements


The following hardware is required for testing a Fibre Channel storage controller. You might need additional hardware if the test device offers other features. To determine whether additional hardware requirements apply, see the test description for each test that appears for the device in Windows HCK Studio.

**Note**  
With the exception of the test computer and test controller, all hardware involved in the test must already have a logo.

 

-   One test computer. The test computer must meet the Windows HCK requirements. For more information, see [Windows HCK Prerequisites](windows-hck-prerequisites.md).

-   One Fibre Channel RAID storage subsystem that can support any one of the following: RAID-0, RAID-1, RAID-5, RAID-10, or RAID-6.

    **Warning**  
    Do not test by using a storage subsystem that connects via MPIO.

     

-   If the Fibre Channel adapter is not bootable, one ATA or SCSI controller.

-   If the Fibre Channel adapter is not bootable, one ATA or SCSI disk drive. The disk must have at least 18 GB of space.

-   One bootable floppy disk drive.

-   One floppy disk.

-   Two identical PCI-X or PCIe-based Fibre Channel adapters (the test devices).

-   Two (or three, if testing RAID-5) Fibre Channel hard disk drives or Fibre Channel JBOD.

-   One PCI-to-PCI bridge adapter.

-   One PCI-to-PCI bridge adapter, unless any of the following conditions apply:

    -   The controllers cannot fit into PCI bridge adapters. This may occur if the controllers are integrated controllers or if the controllers can only fit into specially designed slots.

    -   The controller is designed and sold only for systems that cannot accept full height PCI-to-PCI bridge adapters, such as blade servers.

    -   You can put one of the controllers into a PCI bus slot that is already behind a PCI bridge.

**Note**  
To certify your product for use on servers, the test computer must support four processors and a minimum of 1 GB of RAM. These system capabilities are required to test the Rebalance, D3 State, and Multiple Processor Group functionality of the device and driver. You do not need a computer that actually has more than 64 processors to test your device. Additionally, the server system(s) being used for device or driver testing must have Server Core installed prior to testing. For more information see [Windows Server Installation Options](http://go.microsoft.com/fwlink/p/?LinkID=251454).

If you use a pool of test computers to test devices, at least one computer in the pool must contain four processors and a minimum of 1 GB of RAM. Additionally, that computer must contain the device and the driver that you want to test. If the driver is the same on all the computers in the pool, the system creates a schedule to run against all test computers.

For tests that do not include a driver to test, such as hard disk drive tests, the Windows HCK scheduler constrains the tests that validate the device’s and driver’s rebalance, D3 state, and multiple processor groups functionality to run on the default test computer. You must manually configure this computer to have multiple processor groups. The default computer is the first test computer in the list. Test personnel must make sure that the first test computer in the list meets the minimum hardware requirements.

 

**Note**  
Except for para-virtualization drivers (as defined by Logo Program Requirement Policy-0020), you may not use any form of virtualization when you test physical devices and their associated drivers for server certification or signature. All virtualization products do not support the underlying functionality that is required to pass the tests that relate to multiple processor groups, device power management, device PCI functionality, and other tests.

 

## <a href="" id="bkmk-softwarerequirements"></a>Software Requirements


The following software is required for testing a Fibre Channel storage controller:

-   The drivers for the test device.

-   The latest Windows HCK filters or updates.

-   Windows symbol files. These are available from the [Symbol Files website](http://go.microsoft.com/fwlink/?LinkId=231439).

-   The current release of the Windows Driver Kit (WDK)

## <a href="" id="bkmk-configure"></a>Test Computer Configuration


To configure the test computer to test a Fibre Channel storage controller, follow these steps:

1.  When the test computer is turned off, complete the following assembly steps:

    1.  Install one CD drive in the test system, if the system does not already contain one.

    2.  Install one Fibre Channel adapter (Test Device 1).

    3.  Connect the Fibre Channel adapter to the RAID system.

    4.  If either of the following situations apply, connect two Fibre Channel hard disk drives or a Fibre Channel JBOD to the test device, and then skip to step G:

        -   The Fibre Channel adapter test device is an integrated controller, there is only one of these controllers in the system, and an equivalent PCI adapter version of the device does not exist.

        -   The Fibre Channel adapter is designed for and sold only in a host test system that accepts only a single version of the controller.

        **Note**  
        Use three Fibre Channel hard disk drives for RAID-5 testing.

         

    5.  Install a PCI-to-PCI bridge in a PCI slot in the test system.

        **Note**  
        You can also use an existing slot behind a bridge.

         

    6.  Install a secondary, identical Fibre Channel adapter (Test Device 2) in the PCI-to-PCI bridge card.

    7.  Connect two Fibre Channel hard disk drives or a Fibre Channel JBOD to Test Device 2.

        **Note**  
        Use three Fibre Channel hard disk drives for RAID-5 testing.

         

    8.  Turn on the test computer.

    9.  Configure the JBOD or disks as Array 2, according to the following list:

        -   If the test device supports only one RAID level, configure the JBOD or disks by using that level. Otherwise, configure the JBOD or disks to the RAID levels that are specified in the following table.

            <table>
            <colgroup>
            <col width="50%" />
            <col width="50%" />
            </colgroup>
            <thead>
            <tr class="header">
            <th>RAID levels that the test device supports</th>
            <th>Use RAID level</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td><p>0 and 1</p></td>
            <td><p>1</p></td>
            </tr>
            <tr class="even">
            <td><p>0 and 5</p></td>
            <td><p>5</p></td>
            </tr>
            <tr class="odd">
            <td><p>1 and 5</p></td>
            <td><p>Either 1 or 5</p></td>
            </tr>
            <tr class="even">
            <td><p>0, 1, and 5</p></td>
            <td><p>Either 1 or 5</p></td>
            </tr>
            </tbody>
            </table>

             

        -   Array 2 must contain at least 60 GB of space.

    10. Configure the RAID system as Array 1 according to the following list:

        -   If the RAID system supports only one RAID level, configure it by using that level. Otherwise, configure the RAID system according to the preceding table.

        -   Array 2 must contain at least 60 GB of space.

    11. If the test Fibre Channel adapter is not bootable, install an ATA or SCSI hard disk drive and an alternate ATA or SCSI boot controller if they are not present.

2.  Turn on the test computer, install the appropriate Windows operating system, install all available Windows updates, and then configure the computer for your test network. The test network is the network that contains the Windows HCK Studio and Windows HCK Controller.

3.  Install any HBA or RAID system drivers that are necessary to connect to or manage the peripheral devices.

4.  Do one of the following to install the operating system:

    -   If the test Fibre Channel adapter is bootable, install the operating system on an NTFS, 364-GB partition on the RAID system.

    -   Install the operating system on an NTFS-formatted, 36-GB partition on the ATA or SCSI hard disk drive that is connected to the alternate ATA or SCSI boot controller in the test system.

5.  Start the test system in the Microsoft Windows operating system.

6.  Use the Windows Disk Management utility to set up three 4 GB NTFS partitions on Array 1, as shown in the following diagram:

    ![add-in raid array configuration diagram (client)](images/hck-win8-ata-raid-config-16-1.png)

7.  Use the Windows Disk Management utility to mirror one of the volumes created in step 6 to Array 2.

8.  To set the system page file and enable crashdump, follow these steps:

    1.  Click the **Start** button, right-click **My Computer**, and then click **Properties.**

    2.  Click the **General** tab, and then note the amount of RAM that the computer contains.

    3.  Click the **Advanced** tab (or click **Advanced system settings** in the left pane for Windows Vista, Windows 7, Windows 8, Windows Server 2008, Windows Server 2008 R2 or Windows Server® 2012), and then, in the **Performance** area, click **Settings**.

        **Note**  
        If you are prompted to enter administrative credentials or allow the action, enter the credentials or allow the action.

         

    4.  Click the **Advanced** tab, and then, in the **Virtual Memory** area, click **Change**.

    5.  Select **Custom Size**, and then enter a number in the **Initial size (MB)** box that is larger than the size of RAM that you noted in step b.

    6.  In the **Maximum size (MB)** text box, enter a maximum size value that is larger than the initial size that you entered in the **Initial size (MB)** box. (The maximum size is typically 1.5 to 2 times the initial size.)

    7.  Click **Set**, and then click **OK** two times.

    8.  Click **OK**, and then restart the computer to update the page file size.

9.  Copy the Windows symbol files to %SystemDrive%\\Symbols.

10. Verify that Windows can access the Fibre Channel storage array.

11. Install the Windows HCK client application on the test computer.

12. Use Windows HCK Studio to create a computer pool, and then move the test computer to that pool.

**Warning**  
When testing storage devices, we strongly recommend that you complete all Device Fundamentals tests before starting storage tests. Storage tests will reconfigure your test device, leaving the device in a state unsuitable to support Device Fundamentals tests. The following configurations provide steps to create volume on the storage test device. This is important to complete the Device Fundamental part of testing (DevFund).

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20Fibre%20Channel%20Adapter%20Testing%20Prerequisites%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



