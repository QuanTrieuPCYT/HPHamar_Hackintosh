# HP Hamar Motherboard Hackintosh EFI - macOS 10.13+
OpenCore bootloader (yes, Clover just didn't work) that makes your HP Hamar-powered PC (510-P and 260-P Series) runs macOS High Sierra and up!

![Screen Shot 2021-07-26 at 03 22 27](https://user-images.githubusercontent.com/73286927/126912381-9a32bd51-04a0-4404-b77c-016531467b4c.png)

Also, **your Hack can run Minecraft**.

![Screen Shot 2021-07-21 at 16 24 33](https://user-images.githubusercontent.com/73286927/126465652-c2ff9f2a-b3cf-4186-9d70-820d120d184c.png)

## Motherboard Specs:
![image](https://user-images.githubusercontent.com/73286927/124374625-18f14600-dcc7-11eb-8365-b0313750ff68.png)
* HP/Compaq name: Hamar
* SSID: 81B4
* Chipset: Intel H170
* Processor upgrade information: LGA 1151, accept the following CPU upgrades: `G3900T, G4400T, i3-6100T, i5-6400T and i7-6700T`
* iGPU does not work if a graphics card is installed.
* Ethernet: Realtek RTL8161
* Audio: Realtek ALC867 (layout-id 11)
* Expansion Slots: 1x PCI-E (GEN 3) x16 socket and 1x M.2 socket 1, key A
* 1x HDMI, 2x USB 3.0, 2x USB 2.0 (and another 2x USB 2.0 at the front if HP case is properly installed), 1x VGA (doesn't work in macOS), 1x HDMI, 3x Audio Ports (In, Out and Mic) and 1x Headphone at the front if HP case is properly installed.

**For more detailed info please visit https://support.hp.com/us-en/document/c05066299**

## How to check if my motherboard is compatible?
* **Method 1:** If your HP model name is identical to 510-PXXX(letter) or 260-PXXX(letter) then it's compatible.
* **Method 2:** On Windows press Win+R and type `msinfo32.exe` and scroll down til you can see ur BaseBoard Product. If it's 81B4 then congrats!

## Note:
* iGPU user? Go [here](https://dortania.github.io/OpenCore-Install-Guide/config.plist/skylake.html#deviceproperties) to add your iGPU configuration.
* Update to the latest BIOS version plz (F.42 Rev.A as of 04/07/2021)
* G3900T and G4400T users (like me) will need to fakeID their CPU [(this guide here)](https://github.com/QuanTrieuPCYT/HPHamar_Hackintosh/blob/main/FakeID.md), use a discrete GPU supported in macOS (Intel GT1 iGPU on Celeron and Pentium chips won't gonna work in macOS) and will also need to deal with compatibility issues.
* The Realtek Wi-Fi card that came with most of these 510-P and 260-P series PCs will not gonna work in macOS, so you'll need another card for wireless functionality (Intel or Broadcom M2 cards).
* DRM won't work on iGPU-only systems, so you will need a supported dGPU.
* If your machine came with a dGPU installed, check if it supports macOS, if not then you will need to use your iGPU instead (if it's GT2, GT1 no macOS support as i said earlier). Maxwell and Pascal (maybe Fermi and Tesla) can use their GPU in 10.12 and 10.13 but not 10.14+ and Kepler users can go up to Monterey.
## Tested hardware:
**HP Pavilion Desktop 510-p007l (My main desktop PC)**
* CPU: Intel® Pentium® G4400T (fake ID required)
* RAM: 2x 4GB DDR4 2133MHz
* GPU: GIGABYTE GTX 1050 2GB
* SSD: KingSpec P4-120 120GB SATA SSD (Windows 11)
* HDD: WD Blue WD10EZEX 1TB
* **Runs macOS High Sierra (10.13.6) perfectly (with NVIDIA Web Driver).**

**HP Slimline Desktop - 260-p026 (ENERGY STAR)**
* CPU: Intel® Core™ i3-6100T
* RAM: 2x 8GB DDR4 2133MHz
* GPU: GTX 650
* SSD: Kingston SSDNow V300 120GB SATA SSD
* **Runs macOS Catalina & Big Sur & Monterey perfectly.**

## ✅ Whats workin'
* Graphics acceleration on GT2 iGPUs (HD 530), dGPU (GTX 1050 on 10.13.6, GTX 650 on Monterey)
* USB 2.0 and 3.0 (all)
* Ethernet
* Audio
* SD Card slot (macOS detects it as a normal USB 2.0 device, not a PCI-E card reader so it will work just fine)
* Sleep & Wake (now works with USB mapping)
* CPU Power Management (fixed in 1.1 release)
* iServices (using **this guide: https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html**)
* Wake on LAN
* SMBUS (not important but Intel Power Gadget is useless without SMBUS - the frequency is just maxed out on my G4400T)
## ❌ Not workin'
* iGPU not working when a dGPU is installed
* GT1 iGPU (Intel HD Graphics 510 on Celeron G3900T and Pentium G4400T)
* Realtek Wireless card that came with most of 510-P and 260-P PCs.
* **You tell me**

## FAQ
### Why no Clover?

OpenCore gives you real Mac experience. And it's easy to use too.
I just, don't like Clover. I started Hackintoshing with OpenCore so yeh...

### I saw your EFI drivers folder and i saw `HfsPlusLegacy.efi`. Why would you use that?

Try using the normal `HfsPlus.efi` or the OC-bundled `OpenHfsPlus.efi`. OpenCore will not boot (Clover also).
I spent 4 weeks troubleshooting the issue and tried to replace `HfsPlus.efi` with `HfsPlusLegacy.efi` and turned out IT ACTUALLY WORKED!
Maybe there's a bug that prevents `HfsPlus.efi`/`OpenHfsPlus.efi` from loading, well who knows. Let's just wait for a fix.

### Can't use sleep and my CPU on my hack shows "Unknown"

Told ya before. You are definitely a Celeron/Pentium user. Head over to [this page](https://github.com/QuanTrieuPCYT/HPHamar_Hackintosh/blob/main/FakeID.md) to apply the fixes.

### How to disable verbose boot (those text thingy appear during boot) and use GUI and the Startup Chime?

Remove `-v keepsyms=1	debug=0x100` from `boot-arg`

**Release 1.1** came bundled with GUI. If you want to change the GUI [go here](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html#setting-up-opencore-s-gui)

Follow [this page](https://dortania.github.io/OpenCore-Post-Install/cosmetic/gui.html#setting-up-boot-chime-with-audiodxe) for Boot Chime.

### iServices just didn't work. What should i do?

Follow [this page](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html)

## Credits
* [Apple](https://apple.com) for macOS
* [acidanthera](https://github.com/acidanthera) for OpenCore, Lilu, WhateverGreen and AppleALC
* [Dortania](https://dortania.github.io) for [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide)
* [RehabMan](https://github.com/RehabMan) for USBInjectAll (without this kext i will not be able to map USB)
* [headkaze](https://github.com/headkaze) for Hackintool
* [NVIDIA](https://nvidia.com) for NVIDIA Web Drivers
* And special thanks to [ozonefire1984](https://www.reddit.com/user/ozonefire1984) (ozonefire#0701) for helping me with the EFI (the fakeCPUID patch and more)!

And yes, have a good day!
