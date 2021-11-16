# Born 2 Be Root
[Back To Contents](../../contents.md)
## [Tasks](../index.md) > SSH Server > Setting Up SSH

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

[`Prev`](../../setting-up/setup-sequence/package-management.md "Setting Up > Setup Sequence > Packagement Management") || [`Next`](ssh-firewall.md "Tasks > SSH Server > SSH Firewall")