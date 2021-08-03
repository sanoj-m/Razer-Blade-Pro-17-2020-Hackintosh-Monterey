# Razer-Blade-Pro-17-2020-Hackintosh-Monterey
Note: I'AM NOT RESPONSIBLE IF YOU MESS UP YOUR COMPUTER USING THIS GUIDE!

# Credits to the masters
https://dortania.github.io/OpenCore-Install-Guide/
https://github.com/stonevil
https://github.com/steelbrain

# Support
I have no access anymore to Razer Blade notebooks and not be able to test properly and update documentation. I open for any cooperation and will try maintain this repository as much as possible. Please fill free to create Pull Requests.

# Pre Install

Razer has locked the BIOS tight this time, so you'll need a hardware programmer to unlock DVMT Options this time around. Follow the instructions below for mod your BIOS. After modding the BIOS, change DVMT Pre Alloc to 64MB, DVMT Max Alloc to MAX. Also if you've selected "Dedicated GPU Only" Graphics mode, you'll need to put it back in "NVIDIA (R) Optimus" along with Disabling Secure boot.

# Intro
  
If you would like to get started with creating a Hackintosh on your Razer Blade but have no experience, I would highly reccomend following Dortania's fantastic Opencore Install guide and then returning here for troubleshooting.
  
**Specs**  
| Key | Value |
| :---|  :--- |
| CPU  | Intel Core i7 10875h  |
| GPU  | Intel UHD Graphics 630  |
| Screen | 17" 4K/UHD 120hz Touch Display |
| Camera | HD webcam (720p) |
| RAM | 16 DDR4 2,933MHz (2x8GB) |
| Internal SSD | SSD	1TB M.2 PCIe SSD |
| Audio | ALC298 |
| Wireless | Intel Wireless-AX201 |

Quick Note: My serial number, MLB, and UUID have been removed from the config.plist. Please use CorpNewt's GenSMBIOS to create your own

**What works:**
  
* Trackpad with Gestures  
* Intel Bluetooth / Wifi
* Touchscreen
* Keyboard  
* Backlight Controls  
* All USB Ports including the USB C port  
* Native Audio (Speakers, Headphones, Microphone and Line-In)  
* Sleep  
* Shutdown  
* Restart  
* Camera  
* Battery Status  



# Options and Fixes:
  
**DVMT (All Credits to https://github.com/steelbrain)**
  
The bios from this year's models does not open in AMIBCP. I tried many versions of AMIBCP but they all throw the warning of how language name cannot exceed 0xx bytes.
  
What you want is to download UEFI Tool (but not the new one, the new one opens bios in read-only mode), so download it from https://github.com/LongSoft/UEFITool/releases/tag/0.27.0 then download Universal IFR Extractor (https://github.com/donovan6000/Universal-IFR-Extractor)
  
afterwards you open the BIOS in UEFI Tool and search for "dvmt", it'll point you to a setup blob. Extract that body and save it, then extract it with IFR Extractor. Now open the body blob in a hex editor, I use the online https://hexed.it one
  
The purpose is to unhide the “DVMT Pre Alloc” Settings, there are two parts to it:
  
Finding WHERE the form is hidden
So lookup DVMT in IFR text, see if it’s surrounded in a Suppress If (if so, apply step 2 here), then scroll up to find the parent “FORM”. In my case it was “Graphics Configuration”. The DVMT settings did not have an if/else statement on itself in my case, so I just skip to the parent form. The form “Graphics Configuration” has a form ID of “0x2753” but the hex is 01-86-53-27-BD-06. You’ll see that the order of 0x2753 is 53-27 in shown hex, nothing to worry about. Now search for “53 27” (yes with the space, ‘cause that’s what IFR extractor outputs). You’ll now arrive at a “System Agent Configuration” Form (if you scroll up and see). If you see a Suppress-If surrounding Graphics Configuration, apply second step here. Then lookup the form ID of System Agent Configuration, for me it was “0x2752” with hex of 01-86-52-27-1A-05. Now I look up “52 27” and arrive at the “Chipset” parent Form, that’s where there is a Suppress-If for me. That’s also where you apply the second part.
  
Changing the if/else statement that hides it to be true
In the extracted IFR, you’ll see a lot of “Suppress If” and then on a new line, you’ll see a “Variable X equals Y”. For example for statement, “Variable 0xD98 equals 0x1, the hex would be 12-06-98-0D-01-00”. On the left, there will be a bar of hex in the IFR, that’s the address you can use to jump to in the hex editor.
  
Now you want to look for a menu item that you DO see in the menu, that are not hidden, as-in, the if statement, whatever it is for that, is true. So you want to copy the entire hex for the variable-check from a menu item that is shown, and paste it at the address of the variable check you want to replace.
  
After these changes are done, save the edited file from the hex editor, go to UEFI tool again, right click the Setup blob you extracted and select “Replace body”, then save the updated bios. The bios modding is now complete.
  
Nextup download ASProgrammer from somewhere, clip the CH341A to the BIOS chip and press detect chip, for me I got three choices and it was the second WINBOND something chip. First you want to read from the chip, and save that somewhere as backup. Then you want to open the modded bios, and click the little down arrow next to the “WRITE TO IC” button, that should open up a menu that shows a “Erase, Program, Verify”. Select that! Please note that if you do not erase before you flash, the flasher will just skip over the zeros instead of overwriting them.
  
Another thing to note here is that on my Razer Blade Pro 17 2020, if I disconnected the battery and flashed the bios, the bios would revert to original on boot, so you need to keep the battery plugged in (and the laptop shut down) when you program it.
  
In case you manage to mess up the bios and want a virgin one, go to Razer support, and download any of the “Razer Updater” bios utilities, extract them with peazip or winzip or whatever and you’ll find a vanilla bios in there.
  
After that, just boot into bios and increase the DVMT pre alloc mem. Godspeed!
  
**Caps Lock Light**
  
If you want to map out your keyboard for volume controls and what not without using the FN key this app will do just that: https://pqrs.org/osx/karabiner/  
  **This app will also enable the Caps Lock light.**  
1. Open Karabiner-Elements preferences.
2. Click the Devices TabFind the Razer Blade (Razer) option with the Keyboard Icon underneath the Type column.
3. Check the Manipulate LED box. You will get a warning, just click "Enable LED Manipulation".
4. Save the profile and enjoy the working caps lock light!
