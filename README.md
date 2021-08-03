# Razer-Blade-Pro-17-2020-Hackintosh-Monterey
Note: I'AM NOT RESPONSIBLE IF YOU MESS UP YOUR COMPUTER USING THIS GUIDE!

# Credits
https://github.com/stonevil

# Support
I have no access anymore to Razer Blade notebooks and not be able to test properly and update documentation. I open for any cooperation and will try maintain this repository as much as possible. Please fill free to create Pull Requests.

# Intro
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
  
WiFi & Bluetooth (After network card upgrade)  
Trackpad with Gestures  
Keyboard  
Backlight Controls  
All USB Ports including the USB C port  
Native Audio (Speakers, Headphones, Microphone and Line-In)  
Sleep  
Shutdown  
Restart  
Camera  
Battery Status  



# Options and Fixes:
**Caps Lock Light**  
If you want to map out your keyboard for volume controls and what not without using the FN key this app will do just that: https://pqrs.org/osx/karabiner/  
  **This app will also enable the Caps Lock light.**  
1. Open Karabiner-Elements preferences.
2. Click the Devices TabFind the Razer Blade (Razer) option with the Keyboard Icon underneath the Type column.
3. Check the Manipulate LED box. You will get a warning, just click "Enable LED Manipulation".
4. Save the profile and enjoy the working caps lock light!
