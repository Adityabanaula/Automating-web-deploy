# Automating-web-deploy
Repo to create multiple VM and establish SSH connections. Automate the process of web deployment using Ansible Playbook
## Procedure ##

I have used Vagrant for this project. We can also use any cloud provider like AWS, Azure or GCP.

* Installing Vagrant
    * Installing vagrant is easy. Head over to [Vagrant](https://www.vagrantup.com/downloads) and get the appropriate installer or package for your platform.
      Installer will automatically add `vagrant` to your system path so that it is available in terminals.
    * Vagrant uses VirtualBox for creating VMs. So install VirtualBox from [virtualbox-download](https://www.virtualbox.org/wiki/Downloads) here.

* Setting up multiple VMs
    * Open up the terminal.
    * Git clone the source code or copy the `Vagrantfile` from multi-vagrant-file folder.
        ```
           git clone https://github.com/Adityabanaula/Automating-web-deploy.git
        ```
    * After cloning the repository. Run the following command.
        ```
           vagrant up
        ```
      This command will start creating all three VMs i.e. ansible-VM, web-VM and database-VM.
    
