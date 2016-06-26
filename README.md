# vagrant-docker-aws
A _Vagrant_ _VirtualBox_ which also contains pre-installed _Docker_ and _AWS CLI_ software.

#### Use
This _Vagrant_ _VirtualBox_ is useful for quick testing of miscellaneous Docker-related experiments, or software evaluation.  It also supports deployment of Docker containers from this _Vagrant_ _VirtualBox_ (_vagrantbox_) to any _Amazon Web Service Region_, (_AWS_), via the _AWS_ CLI.

This _Vagrant_ _VirtualBox_ is easy to install, assuming you already have _Vagrant_ and _VirtualBox_ installed.  Because it is a _Vagrant_ _VirtualBox_, it is also easy to remove; simply use the _vagrant destroy_ command, and the trash has been taken out.

I use this _Vagrant_ box for testing my _GitHub_ project _php-server-mon-sys_.  I also use it as an easily discardable host for the demo walk-through script in my _GitHub_ project _presentation-intro-to-devops-for-web-developers_.

#### Installation Requirements

  * Internet connection
  * Hardware virtualizable CPU, dual-core at a minimum
  * 1.2GB available memory is the default.  You may reduce or increase
  * 2GB available disk storage
  * Vagrant 1.8.1, (https://www.vagrantup.com/)
  * VirtualBox 5.0, (https://www.virtualbox.org/)
  * Curl 7.35.0 (or equivalent alternate)
  * UnZip 6.00, (or equivalent alternate)

#### Installation Instructions
The following instructions assume installation and use on an _Ubuntu 14.04_ distribution.  Adapt the instructions for your OS distribution if necessary.

Bringing up this _vagrantbox_ typically takes 9 minutes, but will vary, depending on the speed of your host and Internet connection.

Open a terminal _bash_ session on your host.

Make a project directory and set it as the current directory, e.g. :

      $ mkdir ~/vda-test
      $ cd ~/vda-test

Download the _vagrant-docker-aws_ project ZIP file, named _master.zip_, and then uncompress-unarchive the files from it into your work directory.  The _unzip_ command automatically creates a subdirectory named _vagrant-docker-aws-master_.  Set that directory as the current working directory :

      $ wget -O vagrant-docker-aws.zip https://github.com/addiscent/vagrant-docker-aws/archive/master.zip
      $ unzip vagrant-docker-aws.zip
      $ cd ~/vda-test/vagrant-docker-aws-master
      $ ls -al  # list the vagrant-docker-aws project files
          -rw-rw-r-- 1 usr grp 3.9K Jun  9 05:46 .bashrc
          -rw-rw-r-- 1 usr grp   13 Jun  9 05:46 .gitignore
          -rw-rw-r-- 1 usr grp  12K Jun  9 05:46 LICENSE
          -rw-rw-r-- 1 usr grp 3.5K Jun  9 05:46 README.md
          -rw-rw-r-- 1 usr grp 4.5K Jun  9 05:46 Vagrantfile

Note that you may rename the _vagrant-docker-aws-master_ directory, if you wish.  If you suspect you may rename it sometime in the future, it is best to do so now.

#### Create A New VagrantBox
Use the _vagrant up_ command to create a new _vagrantbox_ containing an instance of _Ubuntu Server 14.04_.  During creation, the _Vagrantfile_ provisioning script also installs _Docker Engine_, _Docker Compose_, _Docker Machine_, and _Amazon Web Services Command Line_ software, (_AWS CLI_) :

      $ vagrant up

Most of the time required for creation of the _vagrantbox_ is consumed by the one-time-only task of downloading the _ubuntu/trusty64_ image from hashicorp.com, and also by the one-time-only installation of the Docker suite and AWS CLI.  When the _vagrant up_ command is used to resume the halted _vagrantbox_ the second time or thereafter, it will load and finish startup in approximately one minute or less.  During creation of the _vagrantbox_, a substantial amount of text is output to the host terminal.  On a terminal with colors enabled, much of the text is green and red.  This is normal.  Vagrant has finished creating the new _vagrantbox_ when the last line of text output shows something similar to :

      ==> default: UnZip 6.00 of 20 April 2009, by Debian. Original by Info-ZIP.

#### Login To The New VagrantBox
When the terminal prompt returns after the new _vagrantbox_ has been created, start an _ssh_ session with the new _vagrantbox_ :

      $ vagrant ssh

In the _ssh_ session created by _vagrant ssh_, the terminal displays some Ubuntu Server 14.04 login banner info, and the following terminal prompt :

      vagrant@vbox-docker-aws:~
      $

Note the name of the currrently logged-in user is _vagrant_.  The user _vagrant_ is the user logged in by default on this _vagrantbox_.

You may need to know the following credentials for some admin activities in this _vagrantbox_ :

      user : vagrant
      password : vagrant

Confirm successful installation of the Docker suite and AWS CLI by entering the following commands and noting the appropriate results:

      $ docker --version
          Docker version 1.11.2, build b9f10c9

      $ docker-compose --version
          docker-compose version 1.7.1, build 0a9ab35

      $ docker-machine --version
          docker-machine version 0.7.0, build a650a40

      $ aws --version
          aws-cli/1.10.37 Python/2.7.6 Linux/3.13.0-87-generic botocore/1.4.27

#### Verify Docker Configuration
_Docker_ installation, including addition of the user _vagrant_ to the group _docker_, is performed by the provisioning script of the _Vagrantfile_, during _vagrant up_.  If _Docker_-related configuration did not complete properly during provisioning, errors occur when attempting to execute _Docker_ commands.  The following "pass/fail" test verifies the configuration is correct for the current user, (in this case, _vagrant_).

      $ docker run hello-world
          Unable to find image 'hello-world:latest' locally
                .
                .
          Hello from Docker.
                .
                .
          For more examples and ideas, visit:
           https://docs.docker.com/engine/userguide/

If _Docker_ is not configured correctly, or if the user _vagrant_ has not been added to the _docker_ group as required, an obvious error message is displayed.  There should be no error message, in this case.

Note the message above shows "Unable to find image 'hello-world:latest' locally".  This is _normal_, because "hello-world" has never been run as a _Docker_ container before on this _vagrantbox_.  When _Docker_ can't find an image locally, _Docker's_ next step is to attempt to download it from the _Docker Hub_ repository named _library/hello_, (https://hub.docker.com).  The message above also contains the phrase, "Hello from Docker".  This is another sign that _Docker_ is configured and functioning correctly.

#### Explore The New VagrantBox
The OS of the newly created _vagrantbox_ is _Ubuntu Server 14.04_.  Explore it in whatever manner you wish, it's simply yet another Linux host, which happens to already have a set of Docker suite and AWS CLI commands installed. Try things you would never feel comfortable doing on a host which in the past took two hours, (or two days), to install and configure.  It's not sacred, it's discardable; if you corrupt it, you may _vagrant destroy_ it, (see _Uninstallation_ below), and recreate a new instance of it just as before, in less than ten minutes.

When you are finished exploring and ready to shut down the _vagrantbox_, exit the _vagrant ssh_ session and return to your host terminal prompt using the usual method :

      $ exit
          logout
          Connection to 127.0.0.1 closed.

#### Uninstallation
The _vagrant destroy_ command removes the _vagrantbox_ instance files, (including the _sysroot_ volume of the _Ubuntu Server 14.04_ _vagrantbox_ itself), from storage on the host.  Any changes previously made to this particular _vagrantbox_ configuration, (e.g., by using a _vagrant ssh_ session to do work such as editing/creating files on the _vagrantbox_ _sysroot_ volume), will be destroyed along with the _vagrantbox_.

The _vagrant destroy_ command does _not_ delete the _vagrant-docker-aws-master_ work/project directory, nor any of the files in that directory :

      $ cd ~/vda-test/vagrant-docker-aws-master
      $ vagrant destroy
            default: Are you sure you want to destroy the 'default' VM? [y/N] y
        ==> default: Forcing shutdown of VM...
        ==> default: Destroying VM and associated drives...

      $ ls -al
          -rw-rw-r-- 1 usr grp 3.9K Jun  9 05:46 .bashrc
          -rw-rw-r-- 1 usr grp   13 Jun  9 05:46 .gitignore
          -rw-rw-r-- 1 usr grp  12K Jun  9 05:46 LICENSE
          -rw-rw-r-- 1 usr grp 3.5K Jun  9 05:46 README.md
          drwxrwxr-x 3 usr grp 4.0K Jun 10 16:17 .vagrant
          -rw-rw-r-- 1 usr grp 4.5K Jun  9 05:46 Vagrantfile

After using the _vagrant destroy_ command, you may then delete from the host the _vagrant-docker-aws-master_ directory, or selected files.

###### Note: Do not delete the files in the project home directory before executing the _vagrant destroy_ command.  The _vagrant destroy_ command is dependent upon reading the _Vagrant_-specific files in the project directory; the _vagrant destroy_ cannot function without those files.  If the _vagrant destroy_ command cannot be executed, orphaned _VirtualBox_ instance files will accumulate in your VirtualBox VM storage directory.  They cause no harm, but may consume large amounts of unnecessary space on host storage.  If you prevent the execution of _vagrant destroy_ by inadvertently deleting the _Vagrant_ files, you may delete orphaned _VirtualBoxes_ using the _VirtualBox GUI_ or _VirtualBox CLI_ commands.

#### Important Common Vagrant Commands

The most important of the commonly used commands are :

      vagrant help
      vagrant up
      vagrant status
      vagrant global-status
      vagrant port
      vagrant suspend
      vagrant resume
      vagrant halt
      vagrant destroy
      vagrant box

#### VagrantBox Memory Allocation
The default _VagrantBox_ memory allocation is 1GB, which may be increased or reduced by revising the _Vagrantfile_.
To do so, revise this _Vagrantfile_ directive :

      vb.memory = "1024"

Change from 1024 to, e.g., 512, or 2048, etc.  Take care to not exceed the host's amount of available real memory.

After revising that directive in the _Vagrantfile_, reload the _vagrantbox_ by executing the following command :

      $ vagrant reload

#### Port Forwarding
If you wish to run a server or app inside _vagrantbox_ which does port IO, such as an NGINX server or a Rails thin web-server, you must configure _Port Forwarding_ on _vagrantbox_.  For a complete discussion, see _Vagrant's_ documentation about _Port Forwarding_ : https://www.vagrantup.com/docs/networking/forwarded_ports.html

To support _php-server-mon-sys_ project, (https://github.com/addiscent), the _Vagrantfile_ contains a directive which forwards _port 28684_ on the _vagrantbox_ to _port 28684_ on the host.

If port forwarding is required for your project, the following _Vagrantfile_ directive is used to configure it.  If port forwarding is not needed for your project, you may remove the directive, by either "commenting it out", or deleting it.

If necessary, change port mapping by revising the _Vagrantfile_, editing the following directive as needed:

      config.vm.network "forwarded_port", guest: 28684, host: 28684

As an example, to change the PSMS application service port on the host, (HTTP port), from 28684 to 8888, revise the directive as :

      config.vm.network "forwarded_port", guest: 28684, host: 8888

After revising that directive in the _Vagrantfile_, reload the _vagrantbox_ by executing the following command :

      $ vagrant reload

#### Where To Go Frome Here?
As installed above, this _vagrantbox_ can be a useful tool, but it has the potential to do much more.

In order to take full advantage of a _vagrantbox_ it is neccesary to learn the _Vagrant_ way of using it on a host.  It's possible to do some _really_ interesting work with _Vagrant/VirtualBox_ instances, but, to do advanced work it is necessary to learn _vagrant_ command line usage, (such as listed above).  It is also necessary to become familiar with the _Vagrantfile_ directives; the _Vagrantfile_ directives noted above are just a few of the many available.

For more information, read the official _Vagrant_ documentation : https://www.vagrantup.com/docs/

In addition to being a provider for _Vagrant_, _VirtualBox_ is very valuable even when used by itself : https://www.virtualbox.org/manual/UserManual.html

#### Advanced Use
##### Shared Storage
There exists a _vagrantbox_ configuration option which allows a file-system directory to be "shared" between the host and a _vagrantbox_.  This allows both the host and the _vagrantbox_ to operate on the same directories and files, (read, write, etc).  As an example, a software developer may edit web page source files on the host, and a _vagrantbox_ HTTP server may deliver them.  This technique is used on the _vagrant-ruby-rails_ project, (https://github.com/addiscent/vagrant-ruby-rails).  For more information, refer to the _Vagrantfile_ directive named "config.vm.synced_folder", in the _Vagrant_ documentation.

##### Custom Provisioning
The _Vagrantfile_ may also be used to do non-trivial configuration of the OS on the _vagrantbox_ during its initial creation, a process known as _Provisioning_.

In order to save yourself time and effort, try to make it a habit to _not_ laboriously create a "pet" _vagrantbox_ instance which is configured by manually installing more "infrastructure" software after it is initially created.  Instead, modify the _Vagrantfile_ with directives and script commands. By doing so, after executing _vagrant up_ the first time, the _vagrantbox_ is already configured the way you need it.

_Vagrant-docker-aws_ provisioning is performed by an _inline_ script, at the end of the _Vagrantfile_.  You may customize the provisioning as needed by editing that section.  An example of what you may wish to include in the provisioning script is the installation of Git.

If you create your own new types of _vagrantboxes_, you may begin to lose a common fear you had in the past, the fear that you "can't try this or that", because it's too risky and may bork your new carefully hand-modified _vagrantbox_.  So, study the _Vagrantfile_ and related documentation.  Experiment with it, customize it to create a _vagrantbox_ which does what you need, from the first _vagrant up_.  Let your mind rest easy, knowing that if you fubar a _vagrantbox_ you are using, you can simply _vagrant destroy_ it, and then quickly "_vagrant up_" a new one, provisioned according to your need.

##### Advanced Architectures
Use of the _config.vm.network_ Vagrantfile directive allows for some interesting experimentation with more advanced architectures. If the host has enough CPU cores and memory, multiple _vagrantboxes_ may be run concurrently.  If you have, say, a four core CPU host with at least 4GB of memory, you can create your own in-memory "virtual server cluster".  It's possible to run three or more _vagrantbox_ instances concurrently, as long as CPU loading is not very heavy.  If you are a student of _Distributed Computing_, Internet, and _Cloud_ technologies, you can learn about _Virtual Networks_ by configuring and running your own networked cluster of servers, all entirely on a single computer, (fair warning: not simple!).  It's a very inexpensive way to teach yourself about advanced computing architectures which can be implemented in the "real world", e.g., on AWS, or a company's networked hardware.

#### Etc
Licensed per Apache License version 2.0

Copyright 2016 Rex Addiscentis raddiscentis@addiscent.com

