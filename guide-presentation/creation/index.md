# Born 2 Be Root
[Back To Contents](../Contents.md)
## Creation
To get Started open `VirtualBox` by Oracle. Click on _New_ and name your machine.
When selecting Type use the `Linux` with the `Debian` option as that is the OS this guide is made for.
Leave the memory at `1024 MB` (`1GB`).

When creating the "Drive", make a `VDI` (Virtual Disk Image) that is Dynamically allocated.
A very important step of the creation of the drive is to
make sure you save it in a place that can store the amount of storage set (which is recommended to be a minimum of 15GB and a maximum of 30GB).
###### DISCLAIMER: Currently a known place is the `goinfre` subdirectory linked on the users home dir (`~/`). If you are going to use the `goinfre` subdirectory to store your VM, remember to stay on that machine for the duration of the project.

After the creation of the drive you are ready to install [**Debian**](../../DEBIAN-Downloads.md "Download Page for Debian Images").
When downloading Debian, it is good practice to keep the ["Image (ISO)"](# "This file acts like a disk") in the same folder and the "Drive (VDI)".
Assuming that you have downloaded a Debian Image you can now attach it to the **VM**.

Enter the VMs **Settings** and navigate to **Storage**. Under `Controller: IDE` Select the icon next to 'Optical Drive'.  
Select `Choose a Virtual Optical Disk File...` and then navigate to your [**'Image'**](# "AKA. '.iso'") of choice.

Still in the settings, go to **Network** > **Advanced Settings** > **Port Forwarding**. Add an entry with the icon on the side and cofigure it as such:  
Name | Protocol | Host IP | Host Port | Guest IP | Guest Port
:-- | :-- | :-- | :-- | :-- | :-- |
Rule 1 | TCP | | 4242 | | 4242

You are now **ready** to get started setting up your VM Environment.

[`Prev`](../introduction/index.md) || [`Next`](../setting-up/background.md "Setting Up > Background")
