# RedHat-RHCE-Notes

## Table of Contents

  - [Introduction](#intro)
  - [Lab Setup](#lab)


## <a name="intro"></a>Introduction 
I passed the RHCSA exam 300/300. Now I am taking on the RHCE certification. This is a compilation of my lab setup, notes, and some playbooks. 

## <a name="lab"></a>Lab Setup
For the lab I decided to use VirtualBox. I downloaded a rhel-9.6.iso with my Red Hat developer account. I setup a control node with a GUI to run ansible and 2 managed nodes with the minimal install (no gui).

***I configured the managed nodes with 2 network interfaces each on their own network for any networking playbooks. I will use the "192" network for the main communication and the "10" network to run the playbooks on***
<p align="center"><img alt="Network" src="RHCE/1networks.png" height="auto" width="800"></p>

***I added an extra hard disk /dev/sdb for partitioning and LVM playbooks. I added the rhel iso to mount it and create a local repository. I also practiced using the control node top mount the rhel iso to host an http repo and connect the nodes to it.***
<p align="center"><img alt="storage" src="RHCE/2storage.png" height="auto" width="800"></p>

***After I had configured everything I made sure to take snapshots, so that I could easily start over with a fresh lab and not have to setup all the minuscule tidbits again. Highly recommend***
<p align="center"><img alt="snapshots" src="RHCE/3snapshots.png" height="auto" width="800"></p>

[Back to Top](https://github.com/HunterCartier702/RedHat-RHCE-Notes/blob/main/README.md)

## <a name="basic"></a>Basic Shell Skills
Vim Basics

```shell
dd # delete current line into memory
yy # copies current line
p # pastes current line(s)
Shft + V # visual mode and you can select blocks of text. d to cut y to copy
Ctrl + v # select characters or group of characters to copy and del with 'd' or 'y'
u # undo last command
Ctrl+r # Redo last command. Only once
?text # search backwards 
^ # go to first position in current line
$ # go to end of line
:%s/old/new/g # replace all occurances of old w/ new. 'gc' to add confirmations
```
