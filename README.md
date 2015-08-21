# vagrant-docker-aws
A _Vagrant_ _VirtualBox_ which includes installed _Docker_ and _AWS CLI_ software.

### Use
This _Vagrant_ _VBox_ is useful for quick testing of miscellaneous Docker-related experiments, or software evaluation, including deploys to _AWS_, (via the _AWS_ CLI).

This _Vagrant_ _VBox_ is easy to install, (assuming you already have _Vagrant_ and _VirtualBox_ installed).  Because it is a _Vagrant_ _VBox_, it is easy to remove; simply use the _vagrant destroy_ command, and the trash has been taken out.

I use this Vagrant box for testing my _GitHub_ project _php-server-mon-sys_, and as an easily discardable host for the demo walk-through script in my _GitHub_ project _presentation-intro-to-devops-for-web-developers_.

### Installation Requirements

  * Vagrant 1.7.2, installed
  * VirtualBox 4.3.10, (or greater), installed

### Installation Instructions
Make a project or scratch directory.  Then, clone the _GitHub_ repo, or download and unzip the _vagrant-docker-aws.zip_ file at:

  * https://github.com/addiscent/vagrant-docker-aws.git

From a terminal prompt in your project host directory, execute:

      $ vagrant up
      $ vagrant ssh

In the _ssh_ terminal created by _vagrant ssh_, the terminal prompt will display something similar to:

      vagrant@vbox-docker-aws:~
      $

Confirm successful installation by entering the following commands and noting the appropriate responses:

      $ docker --version
      Docker version 1.8.1, build d12ea79

      $ docker-machine --version
      docker-machine version 0.4.0 (9d0dc7a)

      $ docker-compose --version
      docker-compose version: 1.4.0

      $ aws --version
      aws-cli/1.7.46 Python/2.7.6 Linux/3.13.0-48-generic

### Uninstallation
Use the _vagrant destroy_ command to ensure _VBox_ disk storage files are removed from host storage.  After using the _vagrant destroy_ command, you may then delete any Vagrant-related files in the project directory from the host.

####### Note: Do not simply delete the files in the project directory, or orphaned _VBox_ files will accumulate in your VirtualBox vm storage area.  They cause no harm, but may use large amounts of unnecessary space on host storage.  You may delete orphaned _VBoxes_ using the VirtualBox GUI or VirtualBox CLI commands.

### Contents Of The VBox
#### Guest OS
Ubuntu Server 14.04 from _Atlas_ (atlas.hashicorp.com/boxes/search) repo, ("ubuntu/trusty64")

#### Additional software installed

  * Docker Engine - latest, (1.8.1, build d12ea79)

  * Docker Machine 0.4.0 (9d0dc7a)

  * Docker Compose 1.4.0

  * AWS CLI - latest, (aws-cli/1.7.45 Python/2.7.6 Linux/3.13.0-48-generic)

  * UnZip 6.00

### Misc
##### VBox Memory Allocation
The default _VBox_ memory allocation is 1GB, which may be changed by revising the Vagrantfile.  _VBox_ provisioning is done by an inline script, at the end of the _Vagrantfile_.

##### Ports
Port 28684 on the _VBox_ is mapped to port 28684 on the host, so _php-server-mon-sys_ works immediately after installation into this _VBox_.  You may change port mapping by revising the _Vagrantfile_.

### Etc
Licensed per Apache License version 2.0

Copyright 2015 Rex Addiscentis raddiscent@addiscent.com
