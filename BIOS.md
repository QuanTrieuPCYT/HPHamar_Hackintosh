# Adjusting BIOS
# In order to get this machine to run macOS, we need to adjust the BIOS and some of its "hidden" settings.

## Adjusting the main BIOS settings
**Enable**

* Intel Virtualization Technology (VT-x)
* Multi-processor
* UEFI Boot
* Execute Disable Bit
* SATA Mode to AHCI

**Disable**

* Legacy ROM support
* Secure Boot
* Intel SGX

## Adjusting hidden BIOS settings
So yeah, here we are, the hardest part.

* Add [`modGRUBShell.efi`](https://github.com/datasone/grub-mod-setup_var/releases/download/1.3/modGRUBShell.efi) and `ControlMsr32.efi` (usually bundled with OC releases, so go grab it by yourself) to `OC/Tools`.
* Boot up your HP with OC, select `modGRUBShell.efi`
* Enter the following commands:

  `setup_var 0xE2 0x00` - Disable CFG Lock
  
  `setup_var 0xE0D 0x01` - Make the iGPU present even when a dGPU is present in the system
  
  `setup_var 0x453 0x02` - Set DVMT Pre-Allocated to `64M`
  
  `setup_var 0x454 0x03` - Set DVMT Total Gfx Mem to `MAX`
  
  `setup_var 0x47D 0x01` - Fully enable the iGPU
 * After entering all of the above commands, type `exit` and power cycle your PC.
## Edit config.plist
**If your HP uses an i3/i5/i7, you have to disable DummyPowerManagement and delete the content of `Cpuid1Data` and `CPUid1Mask` in `config.plist`.**
### iGPU configuration
Open `config.plist`, head over to `PciRoot(0x0)/Pci(0x2,0x0)`

I will not cover the configuration for your dGPU here, you must **do the research yourself**.

#### If you don't have an external graphics card and you have an i3/i5/i7:
* Add `AAPL,ig-platform-id`, type `Data`, value `00001219`

#### If you don't have an external graphics card and you have a Pentium/Celeron CPU:

**NOTE:** Switching to an i3/i5/i7 or installing a supported dGPU is highly recommended. The integrated GPU of these machines **is not** officially supported and you will face some graphical glitches and even kernel panics.
* Add `AAPL,ig-platform-id`, type `Data`, value `01000219`
* Add `framebuffer-patch-enable`, type `Data`, value `01000000`
* Add `igfxfw`, type `Data`, value `02000000`

#### If you have an external graphics card (iGPU will be used for Intel Quick Sync Video):
* Add `AAPL,ig-platform-id`, type `Data`, value `01001219`
* Add `device-id`, type `Data`, value `02190000` **if you are a Celeron/Pentium user**
