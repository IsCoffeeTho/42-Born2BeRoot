# Born 2 Be Root
[Back To Contents](../../contents.md)
## [Tasks](../index.md) > SSH Server > Connecting To VM using SSH

Now that we have configued and setup the necessary system to use SSH, we can finally connect to it using the Terminal on your host computer.

Open up your favourite terminal app on the Host Machine and double check that `OpenSSH client` is installed by doing [__`ssh -V`__](# "Version check for SSH").
We will now need to generate an SSH Key (You can skip this part if you already have a key), run `ssh-keygen -t rsa -b 1024 [-C comment]`.

Right now the VM knows nothing about and SSH Keys so if you attempted to access the machine, you would be prompted for a password every time.
This is where the keys come in, it makes it easier for you to access a machine from another securely.

[`Prev`](ssh-firewall.md "Tasks > SSH Server > SSH Firewall")