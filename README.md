# Automating-web-deploy
Repo to create multiple VM and establish SSH connections. Automate the process of web deployment using Ansible Playbook
## Procedure ##

I have used Vagrant for this project. We can also use any cloud provider like AWS, Azure or GCP.

* Installing Vagrant
    * Installing vagrant is easy. Head over to [Vagrant](https://www.vagrantup.com/downloads) and get the appropriate installer or package for your platform.
      Installer will automatically add `vagrant` to your system path so that it is available in terminals.
    * Vagrant uses VirtualBox for creating VMs. So install VirtualBox from [virtualbox-download](https://www.virtualbox.org/wiki/Downloads) here.

* Creating multiple VMs
    * Open up the terminal.
    * Git clone the source code.
        ```
           git clone https://github.com/Adityabanaula/Automating-web-deploy.git
        ```
    * After cloning the repository. Run the following command.
        ```
           vagrant up
        ```
      This command will start creating all three VMs i.e. ansible-VM `ansible`, web-VM `web` and database-VM `db`.
    
* Setting up Virtual Machines
    
    * Login to `ansible` using the following command
        ```
	     vagrant ssh ansible
        ```
    * Gain root permission.
        ```
           sudo -i
        ```
    * Change the hostname from `ubuntu-bionic` to `ansible`.
        ```
           vim /etc/hostname
        ```
    * Reboot the machine and then log back again. The hostname will be changed to `ansible`.
        ```
           reboot
        ```
    * Adding IP addresses of `web` and `db` machines to host file. Copy IP addresses from Vagrantfile.
        ```
           vim /etc/hosts
        ```
    * Now reboot `ansible` machine.
    * Login to `web` machine and gain root access.
        ```
           vagrant ssh web
           sudo -i
        ```
    * Same as before we will be changing default hostname to `web` and then reboot.
        ```
           vi /etc/hostname
           reboot
       ```
    * Let's do the same thing for `db` machine. First login and gain root.
       ``` 
          vagrant ssh db
          sudo -i
       ```
    * Change default hostname to `db` and then reboot.
       ```
          vi /etc/hostname
          reboot
       ```

* Setting up SSH connection between machines
    
    * Login to `web` and gain root.
       ```
          vagrant ssh web
          sudo -i
       ```
    * We are going to allow ssh connection using password.
       ```
          vi /etc/ssh/sshd_config
       ```
    * Change `PasswordAuthentication` to yes in line 63.
       ```
          :set number
       ```
    * Do the same steps for `db`.
    * Login to `ansible` and try ssh connection to `web` and `db`. Default password for `vagrant` user is vagrant.
       ```
          ssh vagrant@web
          ssh vagrant@db
       ```
    * Now we will generate key for ssh login without password.
       ```
          ssh-keygen
          ssh-copy-id vagrant@web
          ssh-copy-id vagrant@db
       ```
      Enter the password `vagrant` for both.
    * Now we are able to ssh without password. For security we will also change the ssh file in both `web` and `db` to default.
       ```
          ssh vagrant@web
          sudo -i
          vi /etc/ssh/sshd_config
       ```
      Change the `PasswordAuthentication` to no. Do the same for `db`.
     
* Start automation using ansible
    * Now that everything has been setup. Move to the `/vagrant_data` directory.
       ```
          cd /vagrant_data
       ```
    * Check ansible is installed properly.
       ```
          ansible --version
       ```
    * Now run the automation using `ansible-playbook`.
       ```
          ansible-playbook -i inventory playbook.yaml
       ```
      During the time I made this project it threw an error in `Task [Install HTTPD]` as `yum error` "Cannot find a valid baseurl for repo". If it throws the error again. Then follow the steps below.
    * Check if the website is up by copying IP address of `web` and pasting it in url.

* If error in `Task`
      
    * Login to `ansible` machine.
       ```
          vagrant ssh ansible
       ```
    * SSH into `web` machine.
       ```
          ssh vagrant@web
       ```
    * We will be adding Nameservers to the following file.
       ```
          vi /etc/sysconfig/network-scripts/ifcfg-enp0s8
       ```
      Add the following Nameservers in the configuration file.
       ```
          DNS1=10.0.2.2
          DNS2=8.8.8.8
       ```
    * Restart the `NetworkManager` service.
       ```
          systemctl restart NetworkManager
       ```
    * Follow the same step for `db` machine.



