# Installation
To install LXD use snap

		$ snap install lxd

# Configuration
To use LXD you need to have an user in the lxd group

        	# usermod -aG lxd username

To configure LXD run as root

		# lxd init

>Note that the containers are stored by default in /var/lib/lxd

# Basic Commands
## List images
To list all the available images use

		$ lxc image list images:

If we want to list all the debian images available we use

		$ lxc image list images: debian

## Create a container
Creating a container it's really easy, we just use the alias that we get from the previous command and type

		$ lxc launch images:debian/10 grus

>Note that **grus** it's the hostname of the mahcine

## Launching the container
After we create the container you can enter it with a shell using

		$ lxc exec grus -- /bin/bash

>Note that **/bin/bash** can be replaced with anything you want (zsh, csh, fish, etc...)

You can even just run a simgle command buy doing

        $ lxc exec grus -- apt-get update

>Note that we use **apt-get update** cause in the previous commands we used a debian distro

## Moving file
To retrive a file from the container you can do

		$ lxc file pull grus/etc/hosts .

> This will copy the file in **/etc/hosts** from the container **grus** and place it in the current directory of the host

To push a file to the container you can do

		$ lxd file push hosts grus/etc/

> This will copy the file **hosts** from the folder **/etc/** of the container **grus**

## Stopping and removing the container
To stop the container you can do

		$ lxc stop grus

And to delete it use

		$ lxc delete grus
