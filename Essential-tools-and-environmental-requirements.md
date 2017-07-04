# Essential tools and environnemental requirements

The ALA Portal requires several components like Java, Tomcat and Cassandra, as well as web applications that composes the ALA Portal. These softwares can be automatically installed and configured by an [Ansible](http://www.ansible.com/home) playbook, a type of script, developed together with the project. So if you've got an Ubuntu Linux instance up-and-running, you can use Ansible playbooks in the [ala-install](https://github.com/AtlasOfLivingAustralia/ala-install) project to automatically set up and configure the Linux instance into an ALA Portal.

Besides Ansible playbooks, if you don't have a Linux instance ready, or just want to set up a clean on for this ALA Portal, you can consider the following two tools to create a clean instance:

* [Vagrant](http://www.vagrantup.com/): Create and configure a virtual machine to host the ALA portal;
* [VirtualBox](http://www.vagrantup.com/): The container of virtual machines;

The [installation guide](https://github.com/AtlasOfLivingAustralia/documentation/wiki/Installation) assumes one wants to create a Linux instance and configure an ALA portal from scratch. If you want to configure an existing Linux instance(Ubuntu), you may go straight to the [Ansible section](https://github.com/AtlasOfLivingAustralia/documentation/wiki/Installation#ansible) of the installation guide. This tutorial can only be run on UNIX systems (Linux/Mac OS X), given the fact that Ansible is not yet available on Microsoft Windows as 24 Jun 2014.

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

However, in this guide, the [Vagrantfile](https://github.com/AtlasOfLivingAustralia/ala-install/blob/master/vagrant/ubuntu/Vagrantfile) will determine the server configurations for you.

Now you're ready to start the actual installation of the ALA portal.

## Tested environment
* Vagrant 1.6.2 + VirtualBox v4.3.12 r93733 + Ansible 1.6.1 on Mac OS X 10.8.5.