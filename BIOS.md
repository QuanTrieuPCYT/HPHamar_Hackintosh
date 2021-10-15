# Adjusting BIOS
# In order to get this machine run macOS properly, we need to adjust the BIOS and some of its "hidden" settings.

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
