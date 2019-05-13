# Prerequisites
## An OSC account
See the email from Kate.

## Install Singularity
An unprivileged user is not allowed to build a container image on any OSC login
or computing nodes. To continue hands-on exercises, please install Singularity
on your laptop. If you have any difficulty in performing this installation, you
can use remote-build through Singularity on OSC clusters after signing up
Sylabs Cloud Services. However it is more complicated to put your local files
into a container.
### Install on Linux
For Linux users, you can follow [the installation
instruction](https://www.sylabs.io/guides/3.1/user-guide/installation.html#install-on-linux)
from Singularity user guide.

### Install on macOS or Windows
For macOS and Windows users, you can use [Vagrant
boxes](https://app.vagrantup.com/sylabs) mantained by Sylabs.  Please download
and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads),
[Vagrant](https://www.vagrantup.com/downloads.html) and [Vagrant
Manager](http://vagrantmanager.com/downloads/). 

Create and enter a directory to be used with your Vagrant VM in a terminal
```shell
$ mkdir singularity && cd singualrity
```
Pick one Vagrant box and set up the VM
```shell
# Ubuntu 18.04
$ vagrant init sylabs/singularity-3.1-ubuntu-bionic64 
# or CentOS 7
$ vagrant init sylabs/singularity-3.1-centos-7-64

$ vagrant up
```
Start the VM
```shell
$ cd singularity
$ vagrantup ssh
Welcome to Ubuntu 18.04.2 LTS (GNU/Linux 4.15.0-45-generic x86_64)
...
vagrant@vagrant:~$ singularity version
3.1.1-1
```
By default, Vagrant will share your project directory (the directory with the
Vagrantfile) to `/vagrant`.
```shell
vagrant@vagrant:~$ ls /vagrant
Vagrantfile
```
The [step-by-step
instruction](https://www.sylabs.io/guides/3.1/user-guide/installation.html#install-on-windows-or-mac)
can be found in Singularity user guide.

If you have difficulty in the install above, you can download a Ubuntu-based
virtual machine image with pre-installed Singularity from
[here](https://osu.box.com/s/miw48fpllegnx41skwbmo0veokc2bhza) (size: 3.5 GB)
and follow [this
instruction](https://docs.oracle.com/cd/E26217_01/E26796/html/qs-import-vm.html)
to import a VM to an applicane.

## Sylabs Container Services

[Sylabs Container Services](https://cloud.sylabs.io/home) support cotainer build,
sharing, signing and validation.

### Sign-up 
Multiple sign-up options are supported. I will recommend GitHub or GitLab.
![alt text](./sylab_io_signin.png "Sylabs.io Signin")

### Create a access token to authenticate with the services
Click __Account__ | __Access Tokens__ and then enter a label for a new access
token. Put the token into a file in your home directory named
`~/.singularity/sylabs-token`.
