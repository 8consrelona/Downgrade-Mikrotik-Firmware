# Downgrade Mikrotik Firmware
 
 
I managed to downgrade routeros to v6.46.6 by uploading 
routeros-arm-6.46.6.npk to the 'Files' via the web interface and then selecting System -> Packages -> Downgrade. I did not have to press the reset button on the router.
 
**DOWNLOAD ► [https://comlum-profhe.blogspot.com/?augy=2A0Tcb](https://comlum-profhe.blogspot.com/?augy=2A0Tcb)**


 
It's known that routerboot bootloaders versioned higher than 6.46.6 do not boot correctly via dhcp/tftp. **You will need to downgrade the bootloader to 6.46.6 in order to dhcp/tftpboot your hap ac3 device.** One can check check the routerboot/routeros version by running /system routerboard print
 
In the webui, navigate to System -> Packages -> Downgrade. Your device will reboot and downgrade the 'upgrade-firmware' image to 6.46.6. At this stage I'm not sure what magic I did to set 'current-firmware' to 6.46.6.
 
PoE LED
Anybody here who knows how to activate the PoE LED of LAN port # 5?
Via gpio #452 can activate and deactivate the PoE voltage, but the LED (rear side, between port 5 and the USB connector) stays off. It is supposed to signal the PoE voltage presence on port #5 but apparently is driven separately.

@markbirss Thanks. PoE switching is defined in the device tree as a LED. Controlling the power voltage works fine by switching that LED, but the physical LED itself, signaling voltage presence, apparently is separately controlled.
This PoE function on port #5 is missing in Mtik's user manual.
Would be nice to know which gpio controls this LED, so it can be added to the DT.
 
For anyone who wants to flash Mikrotik devices under Windows, I modified Tftpd64 so it's compatible with Mikrotik BOOTP since I had trouble finding any other compatible TFTP / BOOTP software. This should work with v7 and any earlier bootloaders.
 
From Winbox, go to System -> Routerboard menu item. Routerboard window will appear.
Check your Current Firmware and Upgrade Firmware version.
If the Current Firmware version is greater than the Upgrade Firmware version, click on Upgrade button. It will ask to confirm upgrade. Click Yes button to upgrade firmware.
Now reboot MikroTik Router. After reboot you will find that Firmware has been downgraded.
 
Today, all network specialists are somewhat familiar with MikroTik. The company has made great efforts to improve knowledge and technology since its inception and has now become one of the giants of the network and IT world. In this article, we are going to teach you how to downgrade MikroTik RouterOS and Firmware.
 
MikroTik RouterOS is the operating system of the MikroTik Router Board hardware that can be installed on all computers and works as a router with the required features. RouterOS is a stand-alone operating system based on the Linux kernel and in addition to being installed on personal computers, it has also reached consumers in the form of software and hardware packages. The purpose of creating this operating system was to compete with the famous Cisco IOS operating system that is installed on PCs and provide unique features such as routing, firewall, VPN, monitoring, Qos, Hotspot, Load Balancing and other useful services that provide great help to administrators in managing networks. One of the factors for the development of this operating system is its stability in providing services in small, medium and large networks.
 
Firmware is a software program that is usually stored in the flash ROM of a hardware device and provides instructions on how to operate the device. The firmware is responsible for system behaviors when turning on the system. The firmware provides instructions for how the device interacts with other computer components and hardware. Firmware was used in 1967 to edit data on the CPU, with microcodes embedded in it to execute computer instructions. Firmware has expanded over time. So that they are responsible for its behavior since the computer systems are turned on, and this firmware installed on its hardware causes the user to make his commands understandable to the device and hardware.
 
First of all, you need to Find MikroTik RouterOS Architecture Name. To do this, go to the **System** from your Winbox and then choose the **Resources** menu item. Then you will see the following window:
 
In this step, you need to upload the downloaded file to the MikroTik root directory. To do this, go to **Winbox** and click on the **Files**menu item. Then you can see the file list window.
 
In this section, we will provide the downgrade command. To do this, you should go to **Winbox** and choose **System**. Then click on the **Packages**menu item. Now you can see the Package List window.
 
Now you should check your Current Firmware version and if your current Firmware version is greater than the upgrade Firmware version, click on **Upgrade**. Then click**Yes** to confirm the upgrade.
 
In this article, we taught you how to downgrade MikroTik RouterOS and Firmware. If you have a problem with downgrading MikroTik RouterOS and Firmware, you can contact us in the Comments. I hope this tutorial was useful for you.
 
This page describes common procedures across MikroTik RouterBoard routers. If you edit / add information about a specific model, please consider linking to this page to avoid repeating common instructions.
 
This isn't fully true, while the first part looks correct: v7 RouterBoot doesn't work with OpenWrt, the second is not: my SXTsq 5 ac has v6.47.10 factory firmware, RouterOS doesn't allow to downgrade main firmware below factory, but OpenWrt boots and works fine with it!
 
RouterBoards can netboot OpenWrt initramfs .elf (.bin in some instances) images via TFTP. This RAM-based initramfs OpenWrt image is first used to validate the desired OpenWrt version operates properly without overwriting any existing image in the NAND or NOR flash of the RouterBoard.
 
Once you have verified OpenWrt is working on your MikroTik hardware, use the LuCI web interface to permanently flash the appropriate sysupgrade .bin image into the flash of the RouterBoard. In this way, an initial installation is treated exactly the same as a subsequent OpenWrt upgrade.Prior versions of OpenWrt required a subsequent upgrade to once again boot OpenWrt using initramfs: with the current version of OpenWrt that now uses Unsorted Block images (UBI), the initial flash and subsequent upgrades can be performed directly in-place from the LuCI web interface.
 
The bootloader from RouterOS **v7** is not compatible with OpenWrt. If you have it, you will be able to netboot your device and flash OpenWrt, but after it reboots it will go straight to netboot again.If this happens to you, restore RouterOS using Netinstall, downgrade to RouterOS **v6**, and install OpenWrt again.
 
If the OpenWrt table of hardware says 'trunk', the model specific page should explain if 'trunk' already contains the necessary patches for your model or if you need to compile and patch OpenWrt yourself. Compilation / patching is explained further down in this document. If the documentation is old, then the model may work already in a newer release.
 
Since an initramfs image is just a temporary image (only loaded into RAM), it is safe to test a particular version of OpenWrt by netbooting (using DHCP/BOOTP/TFTP) and downloading the initramfs image.  
When you power down your RouterBoard after loading an initramfs file, OpenWrt will simply vanish: a power down and reboot of the RouterBoard will revert to the prior version of firmware that is still in flash of the RouterBoard.
 
If the RAM-based initramfs version you have selected works for you, feel free to try other versions of OpenWrt, such as Latest release or snapshot.  
Once you are happy with the RAM-based operation of OpenWrt, proceed to the step of flashing OpenWrt in order to permanently write OpenWrt into your RouterBoard.
 
Note: MikroTik's bootloader (routerboot) may have a size limitation for TFTP images, approximately 7MiB. If it refuses to accept an initramfs image above that size (it will proceed to boot whatever was already installed in the device), that could be the reason.
 
Routerboards contain the Mikrotik RouterBoot netboot bootloader that will boot over the network and run an OpenWrt initramfs file. The initramfs file is a single file with the whole OpenWrt package: kernel plus filesystem. A RouterBoard has at least three flash partitions: bootloader, kernel and ubi. The MikroTik bootloader is preserved even after OpenWrt is installed into NAND or NOR flash.
 
The freeware Tiny PXE server is a DHCP/TFTP server that implements the RFC951 BOOTP capability. To enable Tiny PXE's rfc951 BOOTP capabilities, rfc951=1 must be set in the [dhcp] section of the Tiny PXE config.ini file.  
Select the OpenWrt initramfs file as the Boot file Filename, un-check the gPXE or iPXE Filename option, select the Option 54 IP address for the ethernet cable you have connected to the RouterBoard, and put Tiny PXE Online.  
if you have problems running Tiny PXE, you may need to turn off your firewall, run Tiny PXE as administrator, or disable all other ethernet/bluetooth/wifi in Network Connections.
 
It is especially important to ensure only one DHCP/BOOTP/TFTP server is running on your network while attempting a netboot since BOOTP has no support for Proxy DHCP or authoritative DHCP - so be sure to disconnect from any other routers before running Tiny PXE.
 
The RouterBoard default boot protocol is BOOTP. You can change the RouterBoot boot protocol from BOOTP to DHCP by using the COM port or RouterOS, as documented in this list of netboot methods. Warning. Not all RouterBoard devices can boot OpenWRT via DHCP.
 
The instructions in this wiki tend to assume you have changed the netboot protocol to DHCP since DHCP netboot is supported by all DHCP servers.  
However, if you have chosen to use a DHCP/BOOTP/TFTP netboot server that supports rfc951 BOOTP such as dnsmasq or Tiny PXE (with rfc951=1 set in the [dhcp] section of the config.ini), any of these netboot methods will work fine without any changes to the Routerboot boot protocol.
 a2f82b0cb4
 
