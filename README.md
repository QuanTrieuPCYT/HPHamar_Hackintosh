# HP Hamar Motherboard - macOS High Sierra and Up
OpenCore bootloader (yes, Clover shit) that makes your HP Hamar-powered PC (510-P and 260-P Series) runs macOS High Sierra and up!

![Screen Shot 2021-07-05 at 3 05 08 AM](https://user-images.githubusercontent.com/73286927/124398075-f0f0f980-dd3d-11eb-9da7-4ef36910349a.png)

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
On Windows press Win+R and type `msinfo32.exe` and scroll down til you can see ur BaseBoard Product. If it's 81B4 then congrats!

## Note:
* Update to the latest BIOS version plz (F.42 Rev.A as of 04/07/2021)
* G3900T and G4400T users (like me) will need to fakeID their CPU, use a discrete GPU supported in macOS (Intel GT1 iGPU on Celeron and Pentium chips won't gonna work in macOS) and will also need to deal with compatibility issues.
* The Realtek Wi-Fi card that came with most of these 510-P and 260-P series PCs will not gonna work in macOS, so you'll need another card for wireless functionality (Intel or Broadcom M2 cards).
* Work is still in progress for sleep and the SD Card Reader.
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
* SD Card slot (macOS detects it as a normal USB 2.0 device, not a PCIE card reader so it will work just fine)
## ❌ Not workin'
* Sleep & Wake
* **You tell me**
