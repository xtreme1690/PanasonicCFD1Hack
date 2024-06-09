# Panasonic CF-D1 Hackintosh
Panasonic CF-D1 MK3 Hackintosh
* This little repo contains a VERY BASIC EFI folder so you can get your Toughbook CF-D1 MK3 working to run Mojave 10.14.6
* NOTE: SMBIOS WILL NEED TO BE MODIFIED (Board Serial/etc..) but the model (MacBookPro13,1) can be left the same! DO YOURSELF A FAVOR AND MAKE SURE YOU DO THIS OR YOU WILL INVITE PROBLEMS AS I HAVE REMOVED SOME VARIABLES I PERSONALLY USED!!
YOU WILL ALSO NEED ANOTHER MAC OR HACKINTOSH TO GET STARTED HERE!

ALSO UNDERSTAND THE EFI PROVIDED HERE COULD BE CONSIDERED A BIT 'janky' - I'VE GOT IT TO BOOT UP BUT IF ANYONE WANTS TO CLEAN IT UP AND SHARE? GO AHEAD! THIS PROVIDED EFI IS TO BE USED AS A STARTING POINT ONLY!!!!!

Specs:
* CPU: Intel Core i5 6300U
* GPU: Intel HD 520 GPU chipset
* RAM: 16GB DDR3 RAM
* HDD: 1TB SATA SSD

WHAT YOU NEED TO DO:
* Get a 16GB USB or higher
* Download the FULL VERSION OF MOJAVE (Its gigabytes in size, not 400MB or so like Apple would give you) (i used OpenCoreLegacyPatcher to download it but there are other tools out there!)
* Place the downloaded Mojave installer into /Applications on the Mac or Hackintosh you'll be using to get the USB setup for the CF-D1
* Download the Unibeast installer for Mojave (Google is your friend ;) )
* Run the Unibeast installer onto your USB drive and ensure you select the UEFI install option. Dont tweak/customise anything.
* Once the installer is done, the EFI partition of your USB is automatically mounted. Delete everything out of there
* Download and then copy the EFI folder in this repo to the EFI partition of your USB - So it will now look like /EFI/CLOVER...etc..
* Configure the config.plist with new MacBook13,1 variables - THIS IS IMPORTANT!!! I used CloverConfigurator for this (I know its frowned upon, but it worked!)
* Eject the USB
* Plug the USB, as well as a external keyboard and mouse into the CF-D1 (Touchscreen wont work properly at this time!)
* Boot the CF-D1, you may need to press the key button on the CF-D1 to get into BIOS and boot-override with the USB.
* Once the Clover boot picker appears, select the Mojave installer. It will then boot-up and you can procceed to install. Once it's installing just let it do it's thing as when the system reboots it will automatically continue so dont touch anything until you see the welcome setup.

WHAT WORKS:
* Wifi (Airportitlwm V2.2.0 for Mojave - installed for you in /EFI/Clover/kexts/other - Also set a ionetworking kext to force load otherwise this didnt work)
* Intel HD 520 Graphics (Platform ID injection all done for you to get it working on Mojave)
* Proper backlight functioning (SSDT_PNLF.aml installed in /EFI/CLOVER/acpi/patched)
* Audio - AppleALC kext required with layout-id=13 boot argument - Done for you in Boot arguments of config.plist!
* USB Ports (Including the USB 3.0 SuperSpeed port)
* Touchscreen - You must use the UPDD software (which isnt free sadly) - Download their identification tool, it will fail and go into 'Manual Mode' - Select the Fujitsu USB Touch Panel option ane enter it as model "Fujitsu USB Touch Panel" , enter your info and request a download. Then install, run the calibration tool (otherwise mouse pointer and stylus positions wont match up) and then touchscreen works nicely as if it were a mouse touchpad, just with a screen! Works on the login screen too! The download they provide will only be for this touchscreen as they program it with the vendor and device ID's for it - You will get a 7 day trial and 200-clicks per boot up to really test things out and for me its working great so i'll be going with that. I did previously try Voodool2c (in fact the kexts are still in the kexts folder) but it didnt seem to work :(

WHAT DOESNT WORK: (Yet! I am investigating! But does not affect systems ability to be booted and used! If anyone wants to contribute please feel free!)
* SD Reader - I have seen some talk online of it maybe being possible, i just havent dug-in yet. Its a PCIe device made by O2 Micro Inc.

* Hidden USB port underneath a panel on top left side - Not sure why, it's just not detected by anything. Perhaps for debugging/factory purposes hence why it's hidden. Though might have something to do with the 'USB Port Replicator' option in BIOS)

* Ethernet Port - Pretty sure i have the right kernel extensions for this but alas no ethernet interface shows up. I dont need Ethernet personally but i'll continue to see if i can get it working and it may very well be needed for iServices

NOT TESTED (Yet!)

* iServices (iCloud, iMessage etc...)

SOME CAUTIONS:
This Toughbook is...well...tough. I could not for the life of me get OpenCore to work, nor even the latest versions of Clover. What i had to do was use a Unibeast installer for Mojave which has Clover 5102 on it, that is the only version i could get to work without stalling or reboot looping.

Why? I THINK this is because this toughbook has no ability for one to disable the dreaded CFGLOCK , running the ControlMsrE2 EFI utility when i was trying OpenCore indicated that the firmware has CFGLOCK enabled on all CPU cores and i cant find a modded bios, nor am i comfortable trying to mod the bios to unlock it. I cant explain why Clover 5102 included on the Mojave Unibeast installer works but it just does so i'll take it. This also means anything newer than Mojave just doesnt seem to want to work, whether on Clover 5102 or newer or OpenCore. If anyone wants to chime in then please feel free! And yes i had cfglock quirks applied when i tried opencore but they didnt work and the system would simply freeze as it tried to start the installer, whether the installer was Mojave or newer (tried all the way up to Ventura)

SMBios used is for a MacBookPro 13,1 (Tried 13,3 and 14,1 when i was trying OpenCore and newer MacOS versions (same with Clover) ) 
