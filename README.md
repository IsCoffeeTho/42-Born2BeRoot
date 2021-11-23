# Born 2 Be Root
[**Picture Version**](#coming-soon)  
[**Step By Step**](guide-presentation/introduction/index.md)

### Contents
  1. [Introduction](#introduction)
  2. [Creation](#creation)
  3. [Setting Up](#setting-up)
     - [Background](#background---headless-machines)
     - [Installation Process](#installation-process)
     - [Setup Sequence](#setup-sequence)
        - [Authorization](#authorization)
        - [Guided Partitioning](#guided-partitioning)
        - [Package Management](#package-management)
  4. [Tasks](#tasks)
     1. [SSH Server](#ssh-server)
        * [Setting up SSH](#setting-up-ssh)
        * [SSH Firewall](#ssh-firewall)
        * [Connecting To VM using SSH](#connecting-to-vm-using-ssh)
  5. [Coming Soon](#coming-soon)

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

After the creation of the drive you are ready to install [**Debian**](DEBIAN-Downloads.md "Download Page for Debian Images").
When downloading Debian, it is good practice to keep the ["Image (ISO)"](# "This file acts like a disk") in the same folder and the "Drive (VDI)".
Assuming that you have downloaded a Debian Image you can now attach it to the **VM**.

Enter the VMs **Settings** and navigate to **Storage**. Under `Controller: IDE` Select the icon next to 'Optical Drive'.  
Select `Choose a Virtual Optical Disk File...` and then navigate to your [**'Image'**](# "AKA. '.iso'") of choice.

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
With selecting your keyboard, if you are not sure about the language type check with your [Country's Keyboard Layout](https://en.wikipedia.org/wiki/Keyboard_layout "Wikipedia Keyboard layout").

The Subject requires you to have your hostname as `<intra-username>42`.
It is recommened to leave the **Domain Name** blank as the machine will auto generate a domain name.

### Setup Sequence
#### Authorization
[Back To Top](#born-2-be-root)  
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
However the `Username for your account:` must be your `<intra-username>`.  
Configure the Timezone to the closest area availble.

#### Guided Partitioning
[Back To Top](#born-2-be-root)  
The Subject requires us to make atleast two encrypted partitions using **LVM** (Logical Volume Manager).  
When prompted select `Guided - use entire disk and set up encrypted LVM`. It will guide through creating the partitions required.
As for the **Partitioning Scheme** select `Separate /home, /var, and /tmp partitions` then navigate over the `<Yes>`.
It Will then start partitioning your **VM**'s drive and this process can take a while (depending on the Drive and Ram size).

After the encryption of the Drive, you will nee a passphrase. The Debian installer we use has a good recommendation:
> A good passphrase will contain a mixture of letters, numbers and punctuation. Passphrases  
> are recommended to have a length of 20 or more characters.  

This is a really good resource for the basics of secure passwords.  
###### Disclaimer: If you mess up the password creation step, you will be forced to re-encrypt your drive.
It is recommended to encrypt the full drive capacity *which will be defaulted into the prompt*.
The system does two more checks to make sure you are fully aware of the changes you made to the drive.

#### Package Management
[Back To Top](#born-2-be-root)  

Every Application you use on your system will either have been provided with the base **OS** or you will have to install it as a *package*.
When prompted to `Scan extra installation media?` simply just select no.
Selecting the mirror location choose the closest region and then the default 'domain', eg. `Australia` > `deb.debian.org`.  
As for the proxy, it is recommended to leave it blank.

If asked to participate in a survey, you can simply ignore it.

After finishing the package mirror selection you will be given a multiselect panel
```ini
[ ] Debian desktop environment
[ ] ... GNOME
[ ] ... Xfce
...
[ ] ... LXQT
[ ] web server
[*] SSH server
[*] standard system utilities
```
Make sure your panel looks similar to the one above.
If so then continue.

Select `<yes>` to Install GRUB boot loader, and install it to the `/dev/sda` dir if possible.
After all is done the system will try to reboot.

## Tasks
### SSH Server
#### Setting up SSH
[Back To Top](#born-2-be-root)  
**S**ecure **SH**ell is a Command Line Tool used to allow *secure* remote access to a server without even being in the same continent.
If you have not done so already, generate an ssh key on the host computer using `ssh-keygen -t rsa -b 2048`.  

Back to the **VM**, we will need to install the `openssh-server` package.
It is good practice to update the package installer, to do so use the command `sudo apt-get update`.
Then to install the **SSH Server** simply run `sudo apt install openssh-server`.

Always double check that a service is running before using it, you will save yourself from debugging the wrong thing and going into loops.
a simple command to check if the SSH server is running `sudo systemctl status ssh`.  
It should return:
```
• ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (XXX)
     Active: active (running) since Ddd YYY-MM-DD HH:MM:SS TMZN; XXX ago
       Docs: man:ssh(8)
             man:sshd_config(5)
    Process: XXX
   Main PID: XXX (sshd)
      Tasks: 1 (limit: XXX)
     Memory: XXX
        CPU: XXX
     CGroup: XXX
     
XXX <intra-username>42 systemd[1]: Starting OpenBSD Secure Shell server...
XXX <intra-username>42 sshd[XXX]: Server listening on 0.0.0.0 port 22.
XXX <intra-username>42 sshd[XXX]: Server listening on :: port 22.
XXX <intra-username>42 systemd[1]: Started OpenBSD Secure Shell server.
```
As long as `grep Active: <<< $(sudo systemctl status ssh)` returns:  
`Active: active (running) since Ddd YYY-MM-DD HH:MM:SS TMZN; XXX ago`  
SSH is running.

Now we have to configure the server to use the ports that **SSH** is meant to run on for the subject (4242),
That means we need edit the *config* file for the SSH Service.
Using `sudo <vim/nano> /etc/ssh/sshd_config` replace `<vim/nano>` with the text editor of choice.
Double check that you are editing the `/etc/ssh/sshd_config` file and not the `.../ssh_config` file.  
Find the line that says `#Port 22` and replace `#Port 22` with `Port 4242` resulting with:
```sh
Include /etc/ssh/sshd_config.d/*.conf

Port 4242
#AddressFamily any
```
Then restart ssh using `service ssh restart` to update the servers port.

#### SSH Firewall
[Back To Top](#born-2-be-root)  
Now we need to allow the port to talk from the **VM** to the network.
We will be using the package [`ufw`](# "Uncomplicated FireWall") to enable and disable communication ports.
Let's start by installing the package by doing `sudo apt install ufw`.

Once installed you can run `ufw allow 4242`, and this will 'Open' the 4242 port needed to run the SSH server.
If you have skipped the [Introduction](#creation) you may need to reallow the Virtual Box Firewall to talk to 4242.
Upon completion you should be able to use the ssh client on the Host machine to connect to the server.

#### Connecting To *VM* using SSH 
[Back To Top](#born-2-be-root)  
Now that we have configued and setup the necessary system to use SSH, we can finally connect to it using the Terminal on your host computer.

Open up your favourite terminal app on the Host Machine and double check that `OpenSSH client` is installed by doing [__`ssh -V`__](# "Version check for SSH").
We will now need to generate an SSH Key (You can skip this part if you already have a key), run `ssh-keygen -t rsa -b 1024 [-C comment]`.

Right now the VM knows nothing about and SSH Keys so if you attempted to access the machine, you would be prompted for a password every time.
This is where the keys come in, it makes it easier for you to access a machine from another securely.

## Submission
[Back To Top](#born-2-be-root)  
*This section is incomplete, either its soon to be written or is being written.*

## Coming Soon
[Back To Top](#born-2-be-root)  
 * A **Picture Version** of this guide is coming soon.
