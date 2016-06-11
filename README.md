# vagrant-docker-aws
A _Vagrant_ _VirtualBox_ which also contains pre-installed _Docker_ and _AWS CLI_ software.

## Use
This _Vagrant_ _VirtualBox_ is useful for quick testing of miscellaneous Docker-related experiments, or software evaluation.  It also supports deployment of Docker containers from this _Vagrant_ _VirtualBox_ (_vagrantbox_) to an _Amazon Web Service Region_, (_AWS_), via the _AWS_ CLI.

This _Vagrant_ _VirtualBox_ is easy to install, assuming you already have _Vagrant_ and _VirtualBox_ installed.  Because it is a _Vagrant_ _VirtualBox_, it is also easy to remove; simply use the _vagrant destroy_ command, and the trash has been taken out.

I use this _Vagrant_ box for testing my _GitHub_ project _php-server-mon-sys_.  I also use it as an easily discardable host for the demo walk-through script in my _GitHub_ project _presentation-intro-to-devops-for-web-developers_.

## Installation Requirements

  * Hardware virtualizable CPU, dual-core at a minimum
  * 1.2GB available memory is the default.  You may reduce or increase
  * 2GB available disk storage
  * Vagrant 1.8.1, (https://www.vagrantup.com/)
  * VirtualBox 5.0, (https://www.virtualbox.org/)

## Installation Instructions
The following instructions assume installation and use on an _Ubuntu 14.04_ distribution.  Adapt the instructions for your OS distribution if necessary.  Bringing up this _vagrantbox_ typically takes 9 minutes, but will vary, depending on the speed of your host and Internet connection.

Open a terminal _bash_ session on your host.

Make a project directory and set it as the current directory, e.g. :

      $ mkdir ~/vda-test
      $ cd ~/vda-test

Download the _vagrant-docker-aws_ project ZIP file, named _master.zip_, and then uncompress-unarchive the files from it into your work directory.  The _unzip_ command automatically creates a subdirectory named _vagrant-docker-aws-master_.  Set that directory as the current working directory :

      $ curl -O -L https://github.com/addiscent/vagrant-docker-aws/archive/master.zip
      $ unzip master.zip
      $ cd ~/vda-test/vagrant-docker-aws-master
      $ ls -al  # list the vagrant-docker-aws project files
          drwxrwxr-x 3 usr grp 4.0K Jun 10 16:17 .vagrant
          -rw-rw-r-- 1 usr grp 3.9K Jun  9 05:46 .bashrc
          -rw-rw-r-- 1 usr grp   13 Jun  9 05:46 .gitignore
          -rw-rw-r-- 1 usr grp  12K Jun  9 05:46 LICENSE
          -rw-rw-r-- 1 usr grp 3.5K Jun  9 05:46 README.md
          -rw-rw-r-- 1 usr grp 4.5K Jun  9 05:46 Vagrantfile

Use the _vagrant up_ command to create a new _vagrantbox_ containing an instance of _Ubuntu Server 14.04_.  During creation, the _Vagrantfile_ provisioning script also installs Docker Engine, Docker Compose, Docker Machine, and Amazon Web Services Command Line software, (AWS CLI) :

      $ vagrant up

Most of the time required for creation of the _vagrantbox_ is consumed by the one-time-only task of downloading the _ubuntu/trusty64_ image from hashicorp.com, and also by the one-time-only installation of the Docker suite and AWS CLI.  When the _vagrant up_ command is used to resume the halted _vagrantbox_ the second time or thereafter, it will load and finish startup in approximately one minute or less.  During creation of the _vagrantbox_, a substantial amount of text is output to the host terminal.  On a terminal with colors enabled, much of the text is green and red.  This is normal.  Vagrant has finished creating the new _vagrantbox_ when the last line of text output shows something similar to :

      ==> default: UnZip 6.00 of 20 April 2009, by Debian. Original by Info-ZIP.

When the terminal prompt returns after the new _vagrantbox_ has been created, start an _ssh_ session with the new _vagrantbox_ :

      $ vagrant ssh

In the _ssh_ session created by _vagrant ssh_, the terminal displays some Ubuntu Server 14.04 login banner info, and the following terminal prompt :

      vagrant@VirtualBox-docker-aws:~
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

## Uninstallation
The _vagrant destroy_ command removes the _vagrantbox_ instance files, (the _sysroot_ volume of the Ubuntu Server 14.04 _vagrantbox_ itself), from storage on the host.  Any changes previously made to this particular _vagrantbox_ configuration, e.g., by using a _vagrant ssh_ session to do work such as editing/creating files on the _vagrantbox_ _sysroot_ volume will be destroyed along with the _vagrantbox_.

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

## Contents Of The VirtualBox
#### Guest OS
Ubuntu Server 14.04 from _Atlas_ (atlas.hashicorp.com/boxes/search) repo, ("ubuntu/trusty64")

#### Additional software installed

  * Docker Engine 1.11.2

  * Docker Machine 0.7.0

  * Docker Compose 1.7.1

  * AWS CLI - latest, (aws-cli/1.10.36 Python/2.7.6 Linux/3.13.0-86-generic botocore/1.4.26)

  * UnZip 6.00

## Misc
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

## Etc
Licensed per Apache License version 2.0

Copyright 2016 Rex Addiscentis raddiscentis@addiscent.com
