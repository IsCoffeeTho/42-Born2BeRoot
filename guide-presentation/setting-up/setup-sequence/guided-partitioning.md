# Born 2 Be Root
[Back To Contents](../../contents.md)
## [Setting Up](../index.md) > Setup Sequence > Guided Partitioning

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

[`Prev`](authorization.md "Setting Up > Setup Sequence > Authorization") || [`Next`](package-management.md "Setting Up > Setup Sequence > Package Management")