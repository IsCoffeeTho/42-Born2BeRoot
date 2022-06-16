# Born 2 Be Root
[**Picture Version**](#coming-soon)  
[**Step By Step**](guide-presentation/introduction/index.md)

&nbsp;

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
4. [Configuring `sudo`](#configuring-sudo)
	- [Installing `sudo`](#installing-sudo)
	- [Adding `sudo` security rules](#adding-sudo-security-rules)
5. [Tasks](#tasks)
	1. [SSH Server](#ssh-server)
		- [Setting up SSH](#setting-up-ssh)
		- [SSH Firewall](#ssh-firewall)
		- [Connecting To **VM** using SSH](#connecting-to-vm-using-ssh)
	2. [Password Policy](#password-policy)
		- [Setting up the Password Policy](#setting-up-the-password-policy)
		- [The Password Policy](#the-password-policy)
		- [Applying Password Policy Timing](#applying-password-policy-timing)
		- [Applying Password Policy Security](#applying-password-policy-security)
	3. [Monitoring Wall](#monitoring-wall)
6. [Submission](#submission)

### Legend
```sh
~> command # refers to a command ran on the VM
```
```sh
-> command # refers to a command ran on the Host Machine
```

&nbsp;

&nbsp;

&nbsp;

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

&nbsp;
___
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

Enter the **VM**s **Settings** and navigate to **Storage**. Under `Controller: IDE` Select the icon next to 'Optical Drive'.  
Select `Choose a Virtual Optical Disk File...` and then navigate to your [**'Image'**](# "AKA. '.iso'") of choice.

Still in the settings, go to **Network** > **Advanced Settings** > **Port Forwarding**. Add an entry with the icon on the side and cofigure it as such:  
| Name   | Protocol | Host IP | Host Port | Guest IP | Guest Port |
| :----- | :------- | :------ | :-------- | :------- | :--------- |
| Rule 1 | TCP      |         | 4242      |          | 4242       |

You are now **ready** to get started setting up your VM Environment.

&nbsp;
___
## Setting Up
[Back To Top](#born-2-be-root)
### Background - Headless Machines
In Computing (Hardware), the head of a machine refers to the Display Monitor.  
When a machine has a monitor connected and its an active display, the device is considered to have a 'Head'

Likewise with a machine that is able to run without any graphical interface,
it is considered that the machine can run in 'Headless mode'.  
A Headless machine runs all the same with a monitor and without.

&nbsp;

### Installation Process
When Booting up the **VM** after the ***Creation*** stage you will be greeted with the  
`Debian GNU/Linux installer menu (BIOS mode)`  
Because we are not using a monitor based machine, select `Install`. Select your mandatory **Lanugage**, then select your **Timezone**.  
With selecting your keyboard, if you are not sure about the language type check with your [Country's Keyboard Layout](https://en.wikipedia.org/wiki/Keyboard_layout "Wikipedia Keyboard layout").

The Subject requires you to have your hostname as `<intra-username>42`.
It is recommened to leave the **Domain Name** blank as the machine will auto generate a domain name.

&nbsp;

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

&nbsp;

#### Guided Partitioning
[Back To Top](#born-2-be-root)  
The Subject requires us to make atleast two encrypted partitions using **LVM** (Logical Volume Manager).  
When prompted select `Guided - use entire disk and set up encrypted LVM`. It will guide through creating the partitions required.
As for the **Partitioning Scheme** select `Separate /home, /var, and /tmp partitions` then navigate over the `<Yes>`.
It Will then start partitioning your **VM**'s drive and this process can take a while (depending on the Drive and Ram size).

After the encryption of the Drive, you will need a passphrase. The Debian installer we use has a good recommendation:
> A good passphrase will contain a mixture of letters, numbers and punctuation. Passphrases  
> are recommended to have a length of 20 or more characters.  

This is a really good resource for the basics of secure passwords.  
###### Disclaimer: If you mess up the password creation step, you will be forced to re-encrypt your drive.
It is recommended to encrypt the full drive capacity *which will be defaulted into the prompt*.
The system does two more checks to make sure you are fully aware of the changes you made to the drive.

&nbsp;

#### Package Management
[Back To Top](#born-2-be-root)  

Every Application you use on your system will either have been provided with the base **OS** or you will have to install it as a *package*.
When prompted to **`Scan extra installation media?`** simply just select no.
Selecting the mirror location choose the closest region and then the default 'domain', eg. `Australia > deb.debian.org` (42Adelaide).  
As for the proxy, it is recommended to leave it blank.

If asked to participate in a survey, you can simply ignore it.

After finishing the package mirror selection you will be given a multiselect panel.  
Select `SSH Server` and `standard system utilities`.
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
Make sure your panel looks similar to the one above, having the same entries selected.  
If so then continue.

Select `<yes>` to Install GRUB boot loader, and install it to the `/dev/sda` dir if possible.
After all is done the system will try to reboot.
___
## Configuring `sudo`
### Installing `sudo`
[Back To Top](#born-2-be-root)  
To install sudo we need to be root, run:
```sh
~> su -
```
and you will be prompted with a password for root,  
we will then need to the `sudo` package using `apt` (**apt**itude)
```sh
(root)~> apt install sudo
```
When prompted `[Y|n]`, just press enter.  
Now we must edit the config file for `sudo` to forceably allow the user to use the `sudo` command.
```sh
(root)~> <vim/nano> /etc/sudoers.d/config
```
replacing `<vim/nano>` with the text editor of choice.  
Now add the following to the file:
```sh
# /etc/sudoers.d/config
<intra username>	ALL=(ALL) ALL
```
you can then exit `vim` or `nano`, then run:
```sh
(root)~> exit
```
and we will dropped back into the user environment.

&nbsp;

### Adding `sudo` security rules
[Back To Top](#born-2-be-root)  
We will be creating the file `/etc/sudoers.d/security`, run:
```sh
~> sudo <vim/nano> /etc/sudoers.d/security
```
There are seven rules we will need to add
```sh
Defaults	passwd_tries=3 # Maximum of three tries
Defaults	badpass_message="Custom Message" # Will print this ___, replace with your own message
Defaults	logfile="/var/log/sudo/sudo.log" # Log access
Defaults	log_input,log_output # Log each action sudo takes
Defaults	iolog_dir="/var/log/sudo" # Place action logs in a specific directory
Defaults	requiretty # Require TTY 
Defaults	secure_path="usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin" # Path of binaries that require sudo access
```
these rules are mandatory

&nbsp;

___
## Tasks
[Back To Top](#born-2-be-root)
* [SSH Server](#ssh-server)
* [Password Policy](#passwrd-policy)

### SSH Server
#### Setting up SSH
[Back To Top](#born-2-be-root)  
**S**ecure **SH**ell is a Command Line Tool used to allow *secure* remote access to a server without even being in the same continent.
If you have not done so already, generate an ssh key on the host computer using `ssh-keygen -t rsa -b 2048`.  

Back to the **VM**, we will need to install the `openssh-server` package.  
It is good practice to update the package installer, to do so use the command:
```sh
~> sudo apt update
```  
Then to install the **SSH Server** simply run `sudo apt install openssh-server`.

Always double check that a service is running before using it, you will save yourself from debugging the wrong thing and going into loops.
a simple command to check if the SSH server is running 
```sh
~> sudo systemctl status ssh
```  
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
when the output matches when the command is ran:
```sh
~> sudo systemctl status ssh | grep Active:
Active: active (running) since Ddd YYY-MM-DD HH:MM:SS TMZN; XXX ago
```
`SSH` is running.

Now we have to configure the server to use the ports that **SSH** is meant to run on for the subject (4242),
That means we need edit the *config* file for the SSH Service.  
Using:
```sh
~> sudo <vim/nano> /etc/ssh/sshd_config
```
replacing `<vim/nano>` with the text editor of choice.
Double check that you are editing the `/etc/ssh/sshd_config` file and not the `.../ssh_config` file.  
Find the line that says `#Port 22` and replace `#Port 22` with `Port 4242` resulting with:
```sh
Include /etc/ssh/sshd_config.d/*.conf

Port 4242
#AddressFamily any
...
```
Then restart ssh to update the server port using: 
```sh
~> sudo service ssh restart
```

&nbsp;

#### SSH Firewall
[Back To Top](#born-2-be-root)  
Now we need to allow the port to talk from the **VM** to the network.
We will be using the package [`ufw`](# "Uncomplicated FireWall") to enable and disable communication ports.
Let's start by installing the package by doing
```sh
~> sudo apt install ufw
```
Once installed you can run:
```sh
~> sudo ufw allow 4242
```
This will 'Open' the 4242 port needed to run the SSH server.
If you have skipped the [Introduction](#creation) you may need to reallow the Virtual Box Firewall to talk to 4242.
Upon completion you should be able to use the ssh client on the **Host Machine** to connect to the server.

&nbsp;

#### Connecting To *VM* using SSH 
[Back To Top](#born-2-be-root)  
Now that we have configured and setup the necessary system to use SSH, we can finally connect to it using the Terminal on your host computer.

Open up your favourite terminal app on the **Host Machine** and double check that `OpenSSH Client` is installed by running
```sh
-> ssh -V
# Version check for SSH
```
We will now need to generate an SSH Key _(You can skip this part if you already have a key)_, run:
```sh
-> ssh-keygen -t rsa -b 1024 [-C comment]
# -t refers to the type of encryption.
# -b refers to the size of the key.
```

Currently the **VM** knows nothing about and SSH Keys so if you attempted to access the machine, you would be prompted for a password every time.
This is where the keys come in, it makes it easier for you to access a machine from another securely.  
Now that we have obtained the key we can *copy* it over to the host using:
```sh
-> ssh-copy-id <intra-username>@127.0.0.1 -p 4242
```
The **VM** now knows about the host machines key and you can use:
```sh
-> ssh <intra-username>@127.0.0.1 -p 4242
```
to access the machine through a terminal.

> **NOTE**  
> If you encounter an error its most likely that the **VM** isn't trusted by the **Host Machine**.  
> If this is the case run:
> ```sh
> -> ssh-keyscan -H 127.0.0.1 >> ~/.ssh/known_hosts
> ```
This guide will now refer to any terminal with access to the **VM** as `~>`, this includes ssh access from the **Host Machine** to the **VM**.

&nbsp;

### Password Policy
#### Setting up the Password Policy
[Back To Top](#born-2-be-root)  
For the password policy we will be using the package `libpam-pwquality`, run:
```sh
~> sudo apt install libpam-pwquality
```
If you are prompted with `[Y|n]` just press enter, this will proceed with the installation.

&nbsp;

#### The Password Policy
[Back To Top](#born-2-be-root)  
Rules regarding the password time:
- Password expiration at 30 Days.
- Password change cooldown to 2 Days.
- Warning a week before expiration.

Rules regard the password security:
- Password length minimum to 10 Characters.
- Password containing atleast one UPPERCASE, one lowercase and one number.
- Filtered character consecutivity of three characters.
- Password must not contain the username
- New passwords must contain at least seven characters not from the previous.

&nbsp;

#### Applying Password Policy Timing
[Back To Top](#born-2-be-root)  
```sh
~> sudo <vim/nano> /etc/login.defs
```
on line 160 we have all the password config variables to edit
```sh
## line 25 ##
PASS_MAX_DAYS	30	# Password expiration at 30 Days.
PASS_MIN_DAYS	2 	# Password change cooldown to 2 Days.
PASS_WARN_AGE	7	# Warning a week before expiration.
```

&nbsp;

#### Applying Password Policy Security
[Back To Top](#born-2-be-root)  
```sh
~> sudo <vim/nano> /etc/pam.d/common-password
```
on line 25 we can append rules 
```sh
## line 25 ##
password        requisite                       pam_pwquality.so retry=3
```
This is a list of the rules with definitions:
```sh
minlen=10           # Minimum password length
ucredit=-1          # A minimum of 1 Uppercase characters needed
dcredit=-1          # A minimum of 1 Digit characters needed
maxrepeat=3         # Disallow more than 3 of the same characters in a row
reject_username     # Disallow the username from the password
difok=7             # Allows after a certain character difference of the previous and new passwords have been met 
enforce_for_root    # Will force the rules upon the root user
```
Append each rule to line 25 without the comments while having a space to seperate them.

&nbsp;

___
## Monitoring Wall
[Back To Top](#born-2-be-root)  
This task gets really tedious, it is recommended to copy from the code bellow and take time to understand how it works.
```sh
#!/bin/bash
arc=$(uname -a) #uname prints basic system information. -a displays all available information
pcpu=$(grep "physical id" /proc/cpuinfo | sort | uniq | wc -l) #search for the lines "physical id" in /proc/cpuinfo and return them. Then sorts the response, removes the duplicates (uniq), does a count of the lines (wc) and prints the number of lines (-l).
vcpu=$(grep "^processor" /proc/cpuinfo | wc -l) #look for lines that start with "processor". count the lines and return them.
fram=$(free -m | awk '$1 == "Mem:" {print $2}') #gets the memory usage (free) in MB (-m). Print the figure in field 2 (print $2) of line Mem.
uram=$(free -m | awk '$1 == "Mem:" {print $3}') #gets the memory usage (free) in MB (-m). Print the figure in field 3 (print $3) of line Mem.
pram=$(free | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')#get the memory usage (free) then divide field 3 by field 2, multiply by 100 and print the result to two decimal places.
fdisk=$(df -BG | grep '^/dev/' | grep -v '/boot$' | awk '{ft += $2} END {print ft}') #df is disk free, -BG shows the result in GB's. look for lines that have /dev/ in them. ignore (-v) lines that have /boot in them. total the amounts in column 2 and print them.
udisk=$(df -BM | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} END {print ut}') #df is disk free, -BM shows the result in MB's. look for lines that have /dev/ in them. ignore (-v) lines that have /boot in them. total the amounts in column 3 and print themn.
pdisk=$(df -BM | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} {ft+= $2} END {printf("%d"), ut/ft*100}') #df is disk free, -BM shows the result in MB's. look for lines that have /dev/ in them. ignore (-v) lines that have /boot in them. total the amounts in column 3 and column 2. divide column 3 by column 2, multiply by 100 and print as a whole number.
cpul=$(top -bn1 | grep '^%Cpu' | cut -c 9- | xargs | awk '{printf("%.1f%%"), $1 + $3}') #top displays CPU utilisation. -bn1 shows the number of iterations top does to get the data. look for lines that start with Cpu. cut column 9. use this information to print to one decimal place the percentage of field 1 plus 3.
lb=$(who -b | awk '$1 == "system" {print $3 " " $4}') #who -b will show the date and time of the last re-boot. print field 3 and 4 with a space between them.
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -eq 0 ]; then echo no; else echo yes; fi) #use lsblk to see if the line lvm is returned. if it is not return no, else return yes. fi closes the if statement.
ctcp=$(ss -neopt state established | wc -l) #ss shows socket statistics, -neopt state established will show you only TCP sessions established. count and return the number of lines.
ulog=$(users | wc -w) #the users command will print the users logged in on a single line. the wc -w command will count the number of words and return the total.
ip=$(hostname -I) #hostname will return the current host name and domain name on a line. -I will show network address of the host.
mac=$(ip link show | grep "ether" | awk '{print $2}') #show MAC (Media Access Control) address of your server. Find row starting with ether and print field 2.
cmds=$(journalctl _COMM=sudo | grep COMMAND | wc -l) #journalctl gets all the journal entries for sudo, filter by COMMAND to get all commands run by sudo then count the lines and return the number.
wall "	#Architecture: $arc
	#CPU physical: $pcpu
	#vCPU: $vcpu
	#Memory Usage: $uram/${fram}MB ($pram%)
	#Disk Usage: $udisk/${fdisk}Gb ($pdisk%)
	#CPU load: $cpul
	#Last boot: $lb
	#LVM use: $lvmu
	#Connections TCP: $ctcp ESTABLISHED
	#User log: $ulog
	#Network: IP $ip ($mac)
	#Sudo: $cmds cmd"
```
###### [Source](https://github.com/markjso/born2BeRoot-commented/blob/main/monitoring.sh)

&nbsp;

___
## Submission
### Signature
[Back To Top](#born-2-be-root)  
On the **Host Machine** make a new folder with a file called `signature.txt`


navigate to the directory with the **VM**s `.vdi` and run:
```sh
-> shasum <myVMname>.vdi
```

&nbsp;

### Evaluation
[Back To Top](#born-2-be-root)  
The subject.pdf outlines some of the tasks that will take place during evaluations

> This section is incomplete, either its soon to be written or is being written.

## Coming Soon
[Back To Top](#born-2-be-root)  
 * A **Picture Version** of this guide is coming soon.
