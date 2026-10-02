# T440pSequoia
EFI Files used to boot MacOS 15.7.9 (MacOS Sequoia) On the Thinkpad T440p.

# DISCLAIMER
This EFI folder is shared as-is for educational and reference purposes. Open-core and Hackintosh modifications carry inherent risks. I am not responsible for any damage, data loss, or bricked devices resulting from the use of this repository. Proceed at your own risk.

# This EFI Was created with Hackmate!
Hackmate is a free automated MacOS EFI creation tool, however it can only by standard go up to MacOS 12 (Monterey) with a 4th Gen intel cpu, So the steps to get MacOS 15.7.9 running were made by me going onward from the premade EFI for MacOS 12. 
https://github.com/hackmatelabs/hackmate

# Important things to note
Wifi: My model uses an intel wifi chip, so this EFI was configured with Itlwm, if your model has one too you need the Heliport app on MacOS itself to be able to use the driver properly. If you have a broadcom chip instead, please replace itlwm.kext inside your /EFI/OC/Kexts folder with IOSkywalkFamily.kext and IO80211FamilyLegacy.kext. Crucial: You must also use OpenCore to block com.apple.iokit.IOSkywalkFamily in your config.plist kernel blocks, or your system will loop-panic on boot! https://github.com/Edwardwich/BCM-WIFI-Sequoia

Bluetooth: IntelBluetoothFirmware.kext is present but unfunctional, youll have to fix Bluetooth yourself.

Audio: Internal speaker works out of the box. The headphone jack is currently non-functional without a post-install script (you will need to install ALCPlugFix to fix the headphone jack node switching).

Display output (Display Port,HDMI etc): Functional (Tested with one monitor connection only)

Intel HD Graphics 4600: To get full hardware acceleration you ***NEED*** To use OCLP(Open core legacy patcher) to patch MacOS into "Accepting" the driver. (If your Thinkpad T440p has an Nvidia Kepler card the same principal applies, simply patch it with OCLP on MacOS).

Serial Number,ROM,MLB,SystemUUID: I have removed my Serial number and other various parts of it to not let everyone use my Serial number, you will need to create your own with a tool called "GenSMBIOS" https://github.com/corpnewt/gensmbios

# Booting 
**NOTE: The Recovery Medium [.Dmg] is NOT included please download the MacOS 15.7.9 Recovery files yourself and paste them onto the usb.**

You will need to Format a Usb stick of your choice with FAT32 !
Once done, copy the provided EFI folder to your Usb Stick.
Poweroff your Thinkpad and Configure Your BIOS

You will need to Disable "Secure Boot" In your BIOS in order to boot the medium.
Once done make sure that your USB containing the EFI folder is sitting at the very top of your boot order!
Afterwards Save the changes and reboot your thinkpad.
If done correctly you should see the OpenCore boot menu picker!

Example:

<img width="4032" height="3024" alt="image" src="https://github.com/user-attachments/assets/f4cb2375-ed54-4683-800d-9835526ae113" />

Boot the "MacOS 15.7.9 Recovery" image straight from that picker.
Once booted you will be greeted by the MacOS recovery screen, Wifi is not yet avaible here as we dont have the heliport app installed yet!
Please use an Ethernet connection to continue with the setup. (Ethernet connection was not yet tested, if not functional please add the IntelMausi.kext into your /EFI/OC/Kext folder. Also make sure to Create a new snapshot of your config.plist with https://github.com/corpnewt/ProperTree In order for MacOS to boot with the enabled drivers)!

Once installed reboot into your installed MacOS Installtion install Opencore legacy Patcher, patch the Intel HD 4600 graphics. Reboot again once done and you should now have a functional MacOS installation for your Thinkpad T440p, Happy hackintoshing!
