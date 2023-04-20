---
layout: single
title: PuTTY as an alternative to "vagrant ssh"
date: 2023-04-19 05:29:00 +0000
categories: vagrant
---

## Setting up PuTTY as an alternative to "vagrant ssh"

1. Install the latest version of PuTTY from [here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

2. Convert the private key of target vagrant box into PuTTY's own format using `PuTTYgen` tool: 

   ```
   Load an existing private key file > Save private key
   ```

   NOTE: The `PuTTYgen` tool is a part of PuTTY installation package. No additional installation is required.

   NOTE: The private key file (`private_key`) can be found in the directory of target vagrant box (e.g., `C:\luftikus74\ubuntu-22.04\.vagrant\machines\default\virtualbox\private_key`).

   NOTE: Without the format conversion, the following error might occur when connecting to the target vagrant box via PuTTY.

   ```
   Unable to use key file "C:\luftikus74\ubuntu-22.04\.vagrant\machines\default\virtualbox\private_key" (OpenSSH SSH-2 private key (old PEM format))
   login as:
   ```

3. Set up a new PuTTY session with the converted private key.

   NOTE: Please make it sure that the SSH port number is set to `2222` if default SSH port forwarding is not overridden in `Vagrantfile`.


4. Log into the target vagrant box with the username `vagrant`.

## References
* [How To Program Blog - Running Vagrant SSH on Windows](https://howtoprogram.xyz/2016/10/22/run-vagrant-ssh-windows/)
