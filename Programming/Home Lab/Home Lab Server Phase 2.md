# Installing Proxmox
Platform for running virtual machines and containers. First we need to flash my laptops, for that I downloaded the ISO from the Proxmox website. Similar to how I first downladed and installed my flavor of Linux: Zorin OS.

We download the ISO to a clean USB drive. 

Not the ARM version, that uses ARM chips, similar to what my Raspberry Pi has. ARM chip use RISC (Reduced Instruction set computer) instruction sets, these are suited for mobile devices and embedded systems. 

Intel chips in contrast use a more complex instruction set CISC, more suited for high performance operations. 

Flashing the iso -> `sha256sum ~/Downloads/proxmox-ve_9.2-1.iso`
sha256sum creates a hash, think of it like a finger print of the contents of the file. Proxmox generates one as well. You use these to compare if you downloaded the right version. 
- checksums are also used by apt when installing software in Linux 

