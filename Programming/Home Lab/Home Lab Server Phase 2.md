# Installing Proxmox
Platform for running virtual machines and containers. First we need to flash my laptops, for that I downloaded the ISO from the Proxmox website. Similar to how I first downladed and installed my flavor of Linux: Zorin OS.

We download the ISO to a clean USB drive. 

Not the ARM version, that uses ARM chips, similar to what my Raspberry Pi has. ARM chip use RISC (Reduced Instruction set computer) instruction sets, these are suited for mobile devices and embedded systems. 

Intel chips in contrast use a more complex instruction set CISC, more suited for high performance operations. 

Flashing the iso -> `sha256sum ~/Downloads/proxmox-ve_9.2-1.iso`
sha256sum creates a hash, think of it like a finger print of the contents of the file. Proxmox generates one as well. You use these to compare if you downloaded the right version. 
- checksums are also used by apt when installing software in Linux 

Now it was time to flash the iso, and for this I used a brand new USB bought specially for this purpose since I am running dd. Commonly known as disk destroy. 
- This command copies raw bytes from a source to a destination, with no file-level interpretation.


`sudo dd if=/home/manu/Downloads/proxmox-ve_9.2-1.iso of=/dev/sdb bs=4M status=progress conv=fsync`
pgrep -a dd, even though I set the argument status=progress, I didn't get any progress indicator so I got scared that maybe the process got stuck and I ruined my USB or the iso file. 

So I ran a new command I leanred. I had used grep in the past to pattern match and cut the noise out of terminal outputs, but during the flashing of the USB I learn about pgrep that helps you find running processes, indeed, the disk destroyer command was there:

```
manu  ~  pgrep -a dd  
2 kthreadd  
1812 /usr/libexec/evolution-addressbook-factory  
1547907 /usr/sbin/uuidd --socket-activation  
2285155 dd if=/home/manu/Downloads/proxmox-ve_9.2-1.iso of=/dev/sdb bs=4M status=progress conv=fsync
```

So I just waited until it was done. 

After this I ran `sync` to flush the write buffers. Another new term. A buffer is a place in memory to store data temporarily as it is moved from one place to another. In this case, we are moving data from my Desktop to the USB and the temporary data was the ISO's information. 

The dd command indicated bs=4M, so chucks of 4 mb. 
- 4 mb of ISO bytes from my disk to the USB. 

Using a website like [BalenaEtcher](https://etcher.balena.io/) could have saved me this step. Which is what I did when I first installed Zorin Os, but now, I am learning Linux and I have to get comfortable reaching for the terminal, plus this taught me a small lesson on Buffers and `pgrep`. 


