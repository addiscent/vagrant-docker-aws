# vagrant-docker-aws
A _Vagrant_ _VirtualBox_ which also contains pre-installed _Docker_ and _AWS CLI_ software.

### Use
This _Vagrant_ _VirtualBox_ is useful for quick testing of miscellaneous Docker-related experiments, or software evaluation.  It also supports deployment of Docker containers from this _Vagrant_ _VirtualBox_ (_vagrantbox_) to an _Amazon Web Service Region_, (_AWS_), via the _AWS_ CLI.

This _Vagrant_ _VirtualBox_ is easy to install, assuming you already have _Vagrant_ and _VirtualBox_ installed.  Because it is a _Vagrant_ _VirtualBox_, it is also easy to remove; simply use the _vagrant destroy_ command, and the trash has been taken out.

I use this _Vagrant_ box for testing my _GitHub_ project _php-server-mon-sys_.  I also use it as an easily discardable host for the demo walk-through script in my _GitHub_ project _presentation-intro-to-devops-for-web-developers_.

### Installation Requirements

  * Hardware virtualizable CPU, dual-core at a minimum
  * 1.2GB available memory is the default.  You may reduce or increase
  * 2GB available disk storage
  * Vagrant 1.8.1, (https://www.vagrantup.com/)
  * VirtualBox 5.0, (https://www.virtualbox.org/)
  * UnZip 6.00, (or equivalent)

### Installation Instructions
The following instructions assume installation and use on an _Ubuntu 14.04_ distribution.  Adapt the instructions for your OS distribution if necessary.

Bringing up this _vagrantbox_ typically takes 9 minutes, but will vary, depending on the speed of your host and Internet connection.

Open a terminal _bash_ session on your host.

Make a project directory and set it as the current directory, e.g. :

      $ mkdir ~/vda-test
      $ cd ~/vda-test

Download the _vagrant-docker-aws_ project ZIP file, named _master.zip_, and then uncompress-unarchive the files from it into your work directory.  The _unzip_ command automatically creates a subdirectory named _vagrant-docker-aws-master_.  Set that directory as the current working directory :

      $ curl -O -L https://github.com/addiscent/vagrant-docker-aws/archive/master.zip
      $ unzip master.zip
      $ cd ~/vda-test/vagrant-docker-aws-master
      $ ls -al  # list the vagrant-docker-aws project files
          -rw-rw-r-- 1 usr grp 3.9K Jun  9 05:46 .bashrc
          -rw-rw-r-- 1 usr grp   13 Jun  9 05:46 .gitignore
          -rw-rw-r-- 1 usr grp  12K Jun  9 05:46 LICENSE
          -rw-rw-r-- 1 usr grp 3.5K Jun  9 05:46 README.md
          -rw-rw-r-- 1 usr grp 4.5K Jun  9 05:46 Vagrantfile

Use the _vagrant up_ command to create a new _vagrantbox_ containing an instance of _Ubuntu Server 14.04_.  During creation, the _Vagrantfile_ provisioning script also installs _Docker Engine_, _Docker Compose_, _Docker Machine_, and _Amazon Web Services Command Line_ software, (_AWS CLI_) :

      $ vagrant up

Most of the time required for creation of the _vagrantbox_ is consumed by the one-time-only task of downloading the _ubuntu/trusty64_ image from hashicorp.com, and also by the one-time-only installation of the Docker suite and AWS CLI.  When the _vagrant up_ command is used to resume the halted _vagrantbox_ the second time or thereafter, it will load and finish startup in approximately one minute or less.  During creation of the _vagrantbox_, a substantial amount of text is output to the host terminal.  On a terminal with colors enabled, much of the text is green and red.  This is normal.  Vagrant has finished creating the new _vagrantbox_ when the last line of text output shows something similar to :

      ==> default: UnZip 6.00 of 20 April 2009, by Debian. Original by Info-ZIP.

When the terminal prompt returns after the new _vagrantbox_ has been created, start an _ssh_ session with the new _vagrantbox_ :

      $ vagrant ssh

In the _ssh_ session created by _vagrant ssh_, the terminal displays some Ubuntu Server 14.04 login banner info, and the following terminal prompt :

      vagrant@vbox-docker-aws:~
      $

You may need to know the following credentials for some admin activities in this _vagrantbox_ :

      user : vagrant
      password : vagrant

Confirm successful installation of Docker and AWS CLI by entering the following commands and noting the appropriate results:

      $ docker --version
      Docker version 1.11.2, build b9f10c9

      $ docker-compose --version
      docker-compose version 1.7.1, build 0a9ab35

      $ docker-machine --version
      docker-machine version 0.7.0, build a650a40

      $ aws --version
      aws-cli/1.10.37 Python/2.7.6 Linux/3.13.0-87-generic botocore/1.4.27

The the OS of the newly created _vagrantbox_ is _Ubuntu Server 14.04_.  Explore it in whatever manner you wish, it's simply yet another Linux host, which happens to already have a set of Docker suite and AWS CLI commands installed. Do things you would never try on a host which took you four hours, (or four days), to install and configure.  It's not sacred, it's disposable; if you corrupt it, you may _vagrant destroy_ it, (see _Uninstallation_ below), and recreate a new instance of it just as before, in less than ten minutes.

For more advanced use, let's say running an Apache server or a Rails server inside the _vagrantbox_, read about "port-forwarding", so you can view HTTP pages from the _vagrantbox_, using your web browser.  Learn to do an easy modification to the _Vagrantfile_, and _walla_, you've got a local webserver which doesn't stomp on the NGINX HTTP port or Rails thin server you were already using on your host. https://www.vagrantup.com/docs/networking/forwarded_ports.html

When you are ready, return to your host terminal prompt using the usual method :

      $ exit
      logout
      Connection to 127.0.0.1 closed.

### Uninstallation
The _vagrant destroy_ command removes the _vagrantbox_ instance files, (the _sysroot_ volume of the Ubuntu Server 14.04 _vagrantbox_ itself), from storage on the host.  Any changes previously made to this particular _vagrantbox_ configuration, (e.g., by using a _vagrant ssh_ session to do work such as editing/creating files on the _vagrantbox_ _sysroot_ volume), will be destroyed along with the _vagrantbox_.

The _vagrant destroy_ command does _not_ delete the _vagrant-docker-aws_ work/project directory, nor any of the files in that directory :

      $ cd ~/vda-test/vagrant-docker-aws-master
      $ vagrant destroy
      $ ls -al
          drwxrwxr-x 3 usr grp 4.0K Jun 10 16:17 .vagrant
          -rw-rw-r-- 1 usr grp 3.9K Jun  9 05:46 .bashrc
          -rw-rw-r-- 1 usr grp   13 Jun  9 05:46 .gitignore
          -rw-rw-r-- 1 usr grp  12K Jun  9 05:46 LICENSE
          -rw-rw-r-- 1 usr grp 3.5K Jun  9 05:46 README.md
          -rw-rw-r-- 1 usr grp 4.5K Jun  9 05:46 Vagrantfile

After using the _vagrant destroy_ command, you may then delete from the host the _vagrantbox_ home directory of _vagrant-docker-aws_, or selected files.

###### Note: Use the _vagrant destroy_ command before deleting a _vagrantbox's_ files or directory; do not simply delete the files in the project directory.  Otherwise, orphaned _VirtualBox_ instance files will accumulate in your VirtualBox vm storage area.  They cause no harm, but may consume large amounts of unnecessary space on host storage.  You may delete orphaned _VirtualBoxes_ using the VirtualBox GUI or VirtualBox CLI commands.

### No Free Lunch
As they say, "There's always a 'However'".  To take full advantage of a _vagrantbox_, it is neccesary to learn the _Vagrant_ way of using it on a host.  It's possible to do some _really_ interesting work with _Vagrant/VirtualBox_ instances, but to do advanced work it is necessary to learn the rules and commands of _Vagrant_.  There are _Vagrant_ commands for typical management, (creating, monitoring, modifying, destroying).  There are _Vagrantfile_ directives for setting the memory size of the instance, and for mapping ports from inside the _vagrantbox_ into the host "port space", (Forwarding Ports), and more.

### When Ready For More Advanced Use
You may also change the _Vagrantfile_ to customize the configuration of the OS during its initial creation, (provisioning).  An example of provisioning may be seen in the _Vagrantfile_ used to create this _vagrantbox_.  Instead of laboriously creating a "custom pet" _vagrantbox_ by manually installing/configuring more software after it is created, modify the _Vagrantfile_ so that the _vagrantbox_ is already configured the way you want immmediately after executing _vagrant up_ the first time.  If you do it this way, you lose the fear you had in the past; the fear that you can't try this or that, because it's "too risky" and may bork my environment.

So, inspect the _Vagrantfile_.  Feel free, the freedom to change it in any way you wish, experiment with it, customize it to do what you want to do, (or want to learn to do).  If you fubar it, you can simply _vagrant destroy_ the _vagrantbox_ and recreate it, without worry, because it's not difficult or time consuming.

The Port Forwarding feature of _Vagrant_ allows for some interesting experimentation with more advanced architectures. If the host has enough memory and cores, multiple _vagrantboxes_ may be run concurrently.  "However", keep in mind that weak hardware need not apply for this job.  For every _vagrantbox_ which is exeuting at any given moment, it requires a CPU core, (and the memory it needs).  The good news is if you have an 8 core host with 8GB of memory, you can experiment with creating your own "four-server cluster".  That sort of thing is easier to create and manage on AWS, but every AWS EC2 instance is billed by the minute.

### Contents Of The VirtualBox
#### Guest OS
Ubuntu Server 14.04 from _Atlas_ (atlas.hashicorp.com/boxes/search) repo, ("ubuntu/trusty64")

#### Additional software installed

  * Docker Engine 1.11.2

  * Docker Machine 0.7.0

  * Docker Compose 1.7.1

  * AWS CLI - latest, (aws-cli/1.10.36 Python/2.7.6 Linux/3.13.0-86-generic botocore/1.4.26)

  * UnZip 6.00

### Misc
##### VirtualBox Memory Allocation
The default _VirtualBox_ memory allocation is 1GB, which may be increased or reduced by revising the _Vagrantfile_.
To do so, revise this Vagrantfile directive :

    _vb.memory = "1024"_.

Change 1024 to, e.g., 512, or 2048, etc.

##### VirtualBox Provisioning
_VirtualBox_ provisioning is done by an _inline_ script, at the end of the _Vagrantfile_.  You may customize the provisioning as needed by editing that section.

##### Port Mapping And Php-Server-Mon-Sys
The following information is only relevant to users of _Php-Server-Mon-Sys_; if you do not use this _vagrantbox_ to run _Php-Server-Mon-Sys_, you may ignore this section.

To support _php-server-mon-sys_, the _Vagrantfile_ contains a directive which maps _Port 28684_ on the _VirtualBox_ to _port 28684_ on the host.  If necessary, change port mapping by revising the _Vagrantfile_, editing the following directive as needed:

  * config.vm.network "forwarded_port", guest: 28684, host: 28684

### Etc
Licensed per Apache License version 2.0

Copyright 2016 Rex Addiscentis raddiscentis@addiscent.com
