# Ryzentosh
MacOS on my custom built PC

# What works
Everything except Airdrop and Facetime

# PC Components
CPU: AMD Ryzen 5 3400G <br />
GPU: AMD Radeon RX 580 <br />
RAM: 16GB DDR4 3200MHz <br />
SSD: 240GB Kingston SSD <br />
USD Wi-Fi Adapter: https://www.amazon.ca/gp/product/B0819HRFL7/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1 <br />
USB Bluetooth Adapter: https://www.amazon.ca/gp/product/B00DJ83070/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1 <br />

# File Download Phase
1.	Checked the computer’s hardware for compatibility
2.	Gathered the required kexts (Kernel Extensions) from https://dortania.github.io/OpenCore-Install-Guide/ktext.html#kexts
3.	Downloaded OpenCore from https://github.com/acidanthera/OpenCorePkg/releases
4.	I have a MacBook Pro 2016 so I downloaded the official installer from the App Store. In case someone does not have an Apple official computer, the installer can be downloaded using gibMacOS (https://github.com/corpnewt/gibMacOS)
5.	Downloaded GenSMBIOS from https://github.com/corpnewt/GenSMBIOS 
6.	Downloaded SSDTTime from https://github.com/corpnewt/SSDTTime
# USB Installer preparation Phase
1.	Created the USB installer
2.	In the USB, added the MacOS installer
3.	Unzipped all the kexts gathered and added all of them to a folder named “Kexts”
4.	Extracted OpenCore (Which gives a folder containing three subfolders: “Docs”, “EFI”, and “Utilities”
5.	Removed “Docs” (only after moving the “Sample.plist” file to the USB under “EFI/OC”) and “Utilities” as they are not needed.
6.	Took the “EFI” folder and moved it into the USB
7.	Went through each folder in “EFI/OC” and only kept “Opencore.efi”, “Bootstrap/Bootstrap.efi”, “Drivers/OpenRuntime.efi”, and “Tools/OpenShell.efi”
8.	Using SSDTTime, unzip the folder and open it in the terminal. From here, I ran the python script and:
  a.	Pressed 4 to dump the system DSDT
  b.	Pressed 1 to patch any IRQ conflicts
  c.	Pressed 2 to make the OS aware of the fake EC
  d.	Pressed 3 to set plugin-type to 1 on CPU0/PR00
      Now MacOS will know the pc’s hardware.
      Under the results folder, took “SSDT-EC.aml”, “SSDT-HPET.aml”, and “SSDT-PLUG.aml” files and moved them to the USB into “EFI/OC/ACPI”.
9.  Rename “Sample.plist” to “config.plist”
10.	Modified the config.plist to work with the hardware and kexts using ProperTree (https://github.com/corpnewt/ProperTree)
11.	At this point all that is left is to generate a serial number and this was done using GenSMBIOS
# Installation Phase
At this point, the boot phase started and a lot of debugging the kernel was done in order to fine tune all the kernel extensions to work perfectly with the components. After three hours of preparation, installation, and debugging, MacOS was finally installed on my custom-built PC!! <br />
One last thing that was done was downloading MountEFI (from https://github.com/corpnewt/MountEFI) and use it to mount the EFI folder on the MacOS installation so that boot was possible without the need of keeping the USB plugged in the PC all the time.
