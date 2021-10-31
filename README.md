# Born 2 Be Root
[**Picture Version**](#coming-soon)
[**Step By Step**](#coming-soon)

### Contents
  1. [Introduction](#introduction)
  2. [Creation](#creation)
  3. [Setting Up](#setting-up)
     - [Background](#background---headless-machines)
     - [Installation Process](#installation-process)
     - [Setup Sequence](#setup-sequence)
  4. [Coming Soon](#coming-soon)

## Introduction
[Back To Top](#born-2-be-root)

**Born 2 Be Root** is a project made to develop the skills of **VM** (**V**irtual **M**achine) or Server creation and maintainence.
This is Skill Set useful for example when you need to have a mini machine to run code continously with or without supervision where it can cause no major harm.

The Subject Documentation goes as follows:
> You will create your first machine in `VirtualBox` (or `UTM` if you can't use `VirtualBox`)
> under specific instructions. Then, at the end of this project, you will be able to set up
> your own operating system while implementing strict rules.
>
> * The use of `VirtualBox` (or `UTM` if you can't use `VirtualBox`) is mandatory.
>
> * You only have to turn in a `signature.txt` file at the root of your repository.
> You must paste in it the signature of your machine’s virtual disk.
> Go to [Submission](#submission) for more information.

## Creation
[Back To Top](#born-2-be-root)

To get Started open `VirtualBox` by Oracle. Click on _New_ and name your machine.
When selecting Type use the `Linux` with the `Debian` option as that is the OS this guide is made for.
Leave the memory at `1024 MB` (`1GB`).

When creating the "Drive", make a `VDI` (Virtual Disk Image) that is Dynamically allocated.
A very important step of the creation of the drive is to
make sure you save it in a place that can store the amount of storage set (which is recommended to be a minimum of 15GB and a maximum of 30GB).
###### DISCLAIMER: Currently a known place is the `goinfre` subdirectory linked on the users home dir (`~/`). If you are going to use the `goinfre` subdirectory to store your VM, remember to stay on that machine for the duration of the project.

After the creation of the drive you are ready to install [**Debian**](<DEBIAN-Downloads.md>).
When downloading Debian, it is good practice to keep the "Image (ISO)" in the same folder and the "Drive (VDI)".
Assuming that you have downloaded a Debian Image you can now attach it to the VM.

Enter the VMs **Settings** and navigate to **Storage**. Under `Controller: IDE` Select the icon next to 'Optical Drive'.  
Select `Choose a Virtual Optical Disk File...` and then navigate to your 'Image' of choice.

Still in the settings, go to **Network** > **Advanced Settings** > **Port Forwarding**. Add an entry with the icon on the side and cofigure it as such:  
Name | Protocol | Host IP | Host Port | Guest IP | Guest Port
:-- | :-- | :-- | :-- | :-- | :-- |
Rule 1 | TCP | | 4242 | | 4242

You are now **ready** to get started setting up your VM Environment.

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
Because we are not using a monitor based machine, select `Install`. Select your mandatory **Lanugage**, then select your **Timezone**.  
With selecting your keyboard, if you are not sure about the language type check with your [Country's Keyboard Layout](https://en.wikipedia.org/wiki/Keyboard_layout).

The Subject requires you to have your hostname as `<intra-username>42`.
It is recommened to leave the **Domain Name** blank as the machine will auto generate a domain name.

### Setup Sequence
Every linux has a permissions system for security of access.
The root user has access to everything, so make sure you keep this password safe.
The Subject states:
> * Your password has to expire every 30 days.  
> * The minimum number of days allowed before the modification of a password will be set to 2.  
> * The user has to receive a warning message 7 days before their password expires.  
> * Your password must be at least 10 characters long. It must contain an uppercase letter and a number.
> Also, it must not contain more than 3 consecutive identical characters.  
> * The password must not include the name of the user.  
> * The following rule does not apply to the root password: The password must have at least 7 characters that are not part of the former password.  
> * Of course, your root password has to comply with this policy.

When creating the 'user' the `Full name for the new user:` can be anything you like,  
However the `Username for your account:` must be your `<inta-username>`.  
Configure the Timezone to the closest area availble.

#### Guided Partitioning
The Subject requires us to make atleast two encrypted partitions using **LVM** (Logical Volume Manager).  
When prompted select `Guided - use entier disk and set up encrypted LVM`. It will guide through creating the partitions required.
As for the **Partitioning Scheme** select `Separate /home, /var, and /tmp partitions` then navigate over the `<Yes>`.
It Will then start partitioning your **VM**'s drive and this process can take a while (depending on the Drive and Ram size).

After the encryption of the Drive, you will nee a passphrase. The Debian installer we use has a good recommendation:
> A good passphrase will contain a mixture of letters, numbers and punctuation. Passphrases  
> are recommended to have a length of 20 or more characters.  

This is a really good resource for the basics of secure passwords.  
###### Disclaimer: If you mess up the password creation step, you will be forced to re-encrypt your drive.

#### ...

## Coming Soon
[Back To Top](#born-2-be-root)

 * A **Picture Version** of this guide is coming soon.
 * This document will also soon be made into a presentation type layout,
