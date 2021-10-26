# Born 2 Be Root
[Picture Version](#coming-soon)
### Contents
  1. [Introduction](#introduction)
  2. [Creation](#creation)
  3. [Setting Up](#setting-up)  
     - [Background](#background---headless-machines)
     - [Installation Process](#installation-process)
  4. 

## Introduction
[Back To Top](#born-2-be-root)

**Born 2 Be Root** is a project made to develop the skills of **VM** (**V**irtual **M**achine) or Server creation and maintainence.
This is Skill Set useful for example when you need to have a mini machine to run code continously with or without supervision where it can cause no major harm.

The Subject Documentation goes as follows
> You will create your first machine in `VirtualBox` (or `UTM` if you can't use `VirtualBox`)
> under specific instructions. Then, at the end of this project, you will be able to set up
> your own operating system while implementing strict rules.
>
> • The use of `VirtualBox` (or `UTM` if you can't use `VirtualBox`) is mandatory.
>
> • You only have to turn in a `signature.txt` file at the root of your repository.
> You must paste in it the signature of your machine’s virtual disk.
> Go to Submission and peer-evaluation for more information.

## Creation
[Back To Top](#born-2-be-root)

To get Started open `Virtual Box` by Oracle. Click on _New_ and name your machine.
When selecting Type use the `Linux` with the `Debian` option as that is the OS this guide is made for.
Leave the memory at `1024 MG` (`1GB`).

When creating the "Drive", make a `VDI` (Virtual Disk Image) that is Dynamically allocated.
A very important step of the creation of the drive is to
make sure you save it in a place that can store the amount of storage set (which is recommended to be a minimum of 12GB).

Currently a known place is the `goinfre` subdirectory linked on the users home dir (`~/`) as noted by 42 Adelaide.

After the creation of the drive you are ready to install [**Debian**](<DEBIAN-Downloads.md>).
When downloading Debian, it is good practice to keep the "Image (ISO)" in the same folder and the "Drive (VDI)".
Assuming that you have downloaded a Debian Image you can now attach it to the VM.

Enter the VMs **Settings** and navigate to **Storage**. Under `Controller: IDE` Select the icon next to 'Optical Drive'.  
Select `Choose a Virtual Optical Disk File...` and then navigate to your 'Image' of choice.

You are now ready to get started setting up your VM.

## Setting Up
[Back To Top](#born-2-be-root)

### Background - Headless Machines
In Computing (Hardware), the head of a machine refers to the Display Monitor. 

When a machine has a monitor connected and its an active display, the device is considered to have a 'Head'

Likewise with a machine that is able to run without any graphical interface,
it is considered that the machine can run in 'Headless mode'.
A Headless machine runs all the same with a monitor and without.


### Installation Process
When Booting up the VM after the ***Creation*** stage you will be greeted with the  
`Debian GNU/Linux installer menu (BIOS mode)`


## Coming Soon
[Back To Top](#born-2-be-root)

A **Picture Version** of this guide is coming soon, stay tuned!
