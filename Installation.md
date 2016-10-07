You need to have a Vagrant file and an Ansible playbook in order to guide Vagrant and Ansible for the automation.

The whole installation, on an INTEL i7 2.66Ghz MacBook Pro (late 2010) with SSD, takes about 30 mins to finish. This includes time for transferring war files over the internet.

To get them, clone the ALA-install repo at <https://github.com/AtlasOfLivingAustralia/ala-install>.

    $ git clone https://github.com/AtlasOfLivingAustralia/ala-install.git
    $ cd ala-install

##Vagrant##

    $ cd vagrant/ubuntu/
    $ vagrant up

At this time, you should see an ubuntu instance up and running if you open VirturalBox:

![VirtualBox UI](/AtlasOfLivingAustralia/documentation/wiki/img/virtual_box.png)

As of 28 May 2014, you might see "default: stdin: is not a tty" in red. This doesn't harm because if you do:

    $ vagrant ssh

You can login to the ubunto instance you've just set up:
![vagrant ssh](/AtlasOfLivingAustralia/documentation/wiki/img/vagrant_ssh.png)

###Memory problem###
In case of memory issue (not enought), you can modifie the vagrant file on Vagrant/ubuntu-Trusty/Vagrantfile : 

    # these machines require some memory to operate the apps
    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
    end 

then, after you have edit the file, simply start your machine : 
    
    vagrant up

##Ansible##
Now you're ready to configure the ubuntu server with Ansible.
To run the Ansible playbook:

    $ cd ../../ansible/
    $ ansible-playbook -i inventories/vagrant/demo-vagrant ala-demo.yml --private-key ~/.vagrant.d/insecure_private_key -u vagrant -s

The playbook should be finished. There might be some minor non-aborting errors which don't harm. In that case, please file an issue so the developers can investigate. Thanks!

![ansible finished](/AtlasOfLivingAustralia/documentation/wiki/img/ansible_finished.png)

The ALA demo portal should be accessible now. For convenience, as in the Vagrantfile the hostname is set as ala.vagrant.dev and it has an IP address 10.1.1.2, adding a line in /etc/hosts:

    10.1.1.2  ala.vagrant.dev

…will allow you to visit the ALA demo portal from the hosting machine.

![vagrant ssh](/AtlasOfLivingAustralia/documentation/wiki/img/ala.vagrant.dev.png)

Congratulations! Your demo ALA portal is up and running.

####Terminating the VM####
When you're happy with the test installation, chances are you need a break so you need to stop the virtual machine. To do so:

    $ cd ../vagrant/ubuntu/
    $ vagrant halt

This command shuts down the running machine Vagrant is managing.
If you want to remove this test instance, at the same directory, do:

    $ vagrant destroy

This will wipe out the virtual machine and all the configuration you have done with Ansible.