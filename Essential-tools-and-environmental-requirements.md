Before installing the ALA portal, you need to have the following tools ready:

* [Vagrant](http://www.vagrantup.com/): Create and configure a virtual machine to host the ALA portal;
* [VirtualBox](http://www.vagrantup.com/): The container of virtual machines;
* [Ansible](http://www.ansible.com/home): Automate the server configuration.

The ALA portal is supposed to be installed and run on a Linux box and this tutorial can only be run on UNIX systems (Linux/Mac OS X), given the fact that Ansible is not yet available on MS Windows.

Using a Macintosh as an example, here are steps to get these tools ready:

1. [Download Vagrant](http://www.vagrantup.com/downloads.html) and install the downloaded package.
1. [Download VirtualBox](https://www.virtualbox.org/wiki/Downloads) and install the downloaded package.
1. To install Ansible, the easiest way is to install via [homebrew](http://brew.sh/). It's also handy to have [the Command Line Tools for Mac OS X](http://osxdaily.com/2014/02/12/install-command-line-tools-mac-os-x/) installed. Once ready, the following commands will install Ansible:
    
        $ brew update
        $ brew install ansible

The recommended server requirements are:
* Virtual machine with Ubuntu 12 or 13.
* 100GB of free disk storage (ideally SSD), the indexing and processing of data consumes space very fast.
* 32 GB RAM.
* 2 CPUs.

However, in this guide, the Vagrant script will designate the server configurations for you.

Now you're ready to start the actual installation of the ALA portal.

####Tested environment####
* Vagrant 1.6.2 + VirtualBox v4.3.12 r93733 + Ansible 1.6.1 on Mac OS X 10.8.5.