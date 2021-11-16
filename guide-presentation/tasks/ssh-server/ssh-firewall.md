# Born 2 Be Root
[Back To Contents](../../contents.md)
## [Tasks](../index.md) > SSH Server > SSH Firewall

Now we need to allow the port to talk from the **VM** to the network.
We will be using the package [`ufw`](# "Uncomplicated FireWall") to enable and disable communication ports.
Let's start by installing the package by doing `sudo apt install ufw`.

Once installed you can run `ufw allow 4242`, and this will 'Open' the 4242 port needed to run the SSH server.
If you have skipped the [Introduction](../../creation/index.md) you may need to reallow the Virtual Box Firewall to talk to 4242.
Upon completion you should be able to use the ssh client on the Host machine to connect to the server.

[`Prev`](setting-up-ssh.md "Tasks > SSH Server > Setting Up SSH") || [`Next`](connecting-over-ssh.md "Tasks > SSH Server > Connecting To VM using SSH")