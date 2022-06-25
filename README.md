# Installation
To install LXD use `snap`

		$ snap install lxd

---

# Configuration
To use LXD you need to have an user in the `lxd` group

        	# usermod -aG lxd username

To configure LXD run as root

		# lxd init

> Note that containers are stored in `/var/lib/lxd` by default

---

# Basic commands
## Listing images
To list all the available images, use

		$ lxc image list images:

Should we want to list all the *Debian* images available, we shall use

		$ lxc image list images: debian

## Creating a container
Creating an LXD container is really easy: we just use the alias that we get from the previous command, and type

		$ lxc launch images:debian/10 grus

> Note that **grus** is the machine hostname

## Configuring a container

### Limiting CPU usage
You can limit container's CPU usage by, for example, the number of cores or CPU percentage

#### Limit CPU by number of cores
   
		$ lxc config set grus limits.cpu 2
     
#### Limit CPU by percentage

		$ lxc config set grus limits.cpu.allowance 20%


### Limiting RAM usage

		$ lxc config set grus limits.memory 4096MB

> Note that you can also specify the RAM usage in kB/GB/TB

## Launching the container
After you created the container, you can access it with a shell using

		$ lxc exec grus -- /bin/bash

> Note that **/bin/bash** can be replaced with anything you want (`zsh`, `csh`, `fish`, etc.)

You can even just run a single command, by typing

		$ lxc exec grus -- apt-get update

> Note that we use **apt-get update** because in the previous commands we used a *Debian* distro

## Moving a file
You can retrieve a file from the container by typing

		$ lxc file pull grus/etc/hosts .

> This will copy the file in **/etc/hosts** from the container **grus** and place it in the current host directory

To push a file into the container, you can do

		$ lxd file push hosts grus/etc/

> This will copy the file **hosts** to the folder **/etc/** of the **grus** container

## Shutting down and removing the container
To shut down the container you can do

		$ lxc stop grus

And to delete it use

		$ lxc delete grus
