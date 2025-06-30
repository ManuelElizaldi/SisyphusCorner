[[Storage]] [[Linux]] [[CLI]] [[SSD]]

Command `lsblk`:
list all block devices. Block devices are data storage devices that manage data in fixed size segments called blocks.
![[Pasted image 20250630143313.png]]

The name of the SSD is automatically assigned when you plug it in. 

`ls -l` listing directories in long format -> adds details

Our hard drive is stored in the /dev directory 

Drives can have partitions, in the CLI you can target the whole drive or one partition. 
- if you want to check out the partitions of a drive: `sudo fdisk -l`

## Partitions 
*Partitions* are the different sections of a hard drive. Logically divided section of a physical storage device. 
- Each partition can be formatted separately 
- Each can have a different file system 
- Each can be mounted differently

We do this to be more organized and efficient. Usually systems boot from a partition that is not used for storage. Also this keeps data isolated. You can create a back up in a separate partition. 

Once you enter the command `sudo fdisk /your/path` you can create different partitions like these:

#note This table was obtained by pressing m after the fdisk command 
![[Pasted image 20250630145334.png]]

In the [video](https://www.youtube.com/watch?v=2Z6ouBYfZr8) I followed/watched the guy recommended GPT because it can handle more disks. 

I entered `g` to create the *partition table* and then `p` to print the partitions. 

*partition table* -> table of contents for your storage device. It tells you:
- How many partitions there are
- Where each one starts and ends
- What type of data each partition holds 
- If its bootable 

## Creating a partition
`sudo fdisk /dev/sda` -> replace /dev/sda with the path to your hard drive. 

This will show up:
![[Pasted image 20250630144730.png]]
Right now, in the above picture, I have not set up a partition yet. So it does not recognize any. 

After doing `fdisk` we do `n` and the system walks you through the process of doing this. 

It asks you for a partition number. Since this is the first time we create a partition on this drive, it defaults to 1:
![[Pasted image 20250630150040.png]]

Then there's an input for *first sector* you can also press enter here. No need to change it 

After this, *last sector* input is shown, since we want to cover the entire disk, we don't set a last sector and just hit enter. 

like so:
![[Pasted image 20250630150521.png]]

We now can see that the size of the partition is 1.8 Tib (almost 2T). 

#note All of this changes wont be saved unless you *finalize*. 

I did p to print the new partition, then `w` to finalize my changes
![[Pasted image 20250630150809.png]]

## mkfs - Formatting Hard Drive - Attaching a file system 
There are multiple file systems you can use for your storage device. Which one you choose depends on how you are going to use it. 

You always format the partition. 

I asked ChatGPT which file system to use based on my needs (high compatibility) and it recommended exFAT. 

To use exFAT I had to install the dependencies:
```
sudo apt install exfatprogs
```

#note: exFAT is a Microsoft technology

This file system will allows us to communicate to this hard drive through other OSs 

## Mounting Hard Drive
`mount` -> mounted storage devices on a system
- mount | grep *name of your drive*
- mounted device means that the device's file system is connected to the system's directory tree
- for example, when I did `mount | grep sda` at first I didn't get an output because my hard drive is not mounted yet

Before mounting, you have to create the appropriate mount point. Linux has a dedicated directory for this:
- /mnt
	- in here we created another folder /ssd to mount our hard drive. 

Mounting happens in a folder. You can choose any folder, but its a *best practice* to do it the way mentioned above. 
- /media is another appropriate mount point

#note: Mounting is done automatically in PCs and laptops, but since we are running this in a server, we had to mount it manually. 

### When to use /media vs /mnt
- /media is for temporary storage. Something that wont be attached full time. Maybe another hard drive for back up utility, USBs, etc. 
- /mnt is for something that is permanent. <- This is my use case

## Managing Storage
`df -h` -> This command gives you information on all the drives in your system and it also lets you know if the ssd is mounted.

![[Pasted image 20250630153744.png]]

The best command to manage your hard drives `ncdu`. Although it needs to be installed. 
```
sudo apt install ncdu
```

Always install this in any new installation of Linux. You might need this later down the road to trouble shoot. According to the video I am watching -> you might not be able to install this software if your hard drive is already full. 

Always run ncdu with sudo:
```
sudo ncdu /
```

It will scan your machine and then give you an output like so:
![[Pasted image 20250630155229.png]]


`sudo ncdu / -x` excludes any external hard drives 

## Auto Mounting Hard Drive on Boot

the file */etc/fstab* contains the root file system. You need to modify this file and add the hard drive that you want to be automatically mounted on boot.
#### You have to be careful modifying this file. If you change something that you shouldn't, the system might not boot.

This will give you the contents of the file: 
```
cat /etc/fstab
```
### Here's what we did to add our ssd to the fstab file:

To modify the *fstab* file:
```
sudo nano /etc/fstab
```

we did:
```
sudo blkid
```

to get the partition details:
```
/dev/sda1: UUID="6AEA-F2E6" BLOCK_SIZE="512" TYPE="exfat" PTTYPE="dos" PARTUUID="6f6ec423-59dc-4c47-aead-4ab0ed6b6489"
```

We add these details to the file and this will allow it to auto mount on boot. 

To check if there's any errors we run:
```
sudo mount -a
```

the command above mounts everything in the /etc/fstab file except the ones marked with noauto. If there's an error it means the config file needs to be modified. 


## Unmounting a Hard Drive

You simply do `lsblk` to get the mount point of the SSD, then use that path in:

`sudo umount /mount/point`

and you'll successfully unmount 



---- 
##### Source
https://www.youtube.com/watch?v=2Z6ouBYfZr8
