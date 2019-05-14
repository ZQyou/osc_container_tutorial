# Prerequisites
## Get an OSC account
See the email from Kate.

## Install Singularity
An unprivileged user is not allowed to build a container image on any OSC login
or computing node. To continue hands-on exercises, please install Singularity
on your laptop. If you have any difficulty in performing this installation, you
can use remote-build through Singularity on OSC clusters after signing up
Sylabs Cloud Services. However it is more complicated to put your local files
into a container.
### Install on Linux
For Linux users, you can follow [the installation
instruction](https://www.sylabs.io/guides/3.1/user-guide/installation.html#install-on-linux)
from Singularity user guide or [this
one](https://github.com/sylabs/singularity/blob/master/INSTALL.md) from
Singularity source code.

Here is my quick install note
```shell
# Install system dependencies
$ sudo apt-get update 
$ sudo apt-get install -y build-essential libssl-dev \
  uuid-dev libgpgme11-dev squashfs-tools libseccomp-dev

# Install Go
$ cd /tmp
$ wget https://dl.google.com/go/go1.12.5.linux-amd64.tar.gz
$ sudo tar xf go1.12.5.linux-amd64.tar.gz -C /usr/local

# Install Singluarity
$ mkdir -p $HOME/go/src/github.com/sylabs
$ cd $HOME/go/src/github.com/sylabs
$ wget https://github.com/sylabs/singularity/releases/download/v3.1.1/singularity-3.1.1.tar.gz
$ tar xf singularity-3.1.1.tar.gz
$ cd singularity
$ ./mconfig
$ cd builddir
$ PATH=/usr/local/go/bin:$PATH make
$ sudo make install
```


### Install on macOS or Windows
For macOS and Windows users, you can use [Vagrant
boxes](https://app.vagrantup.com/sylabs) mantained by Sylabs. Please download
and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads),
[Vagrant](https://www.vagrantup.com/downloads.html) and [Vagrant
Manager](http://vagrantmanager.com/downloads/). 

Create and enter a directory to be used with your Vagrant VM in a terminal
```shell
$ mkdir singularity && cd singualrity
```
Pick one Vagrant box and set up the VM
```shell
$ vagrant init sylabs/singularity-3.1-ubuntu-bionic64 && vagrant up
```
Start the VM
```shell
$ cd singularity
$ vagrantup ssh
Welcome to Ubuntu 18.04.2 LTS (GNU/Linux 4.15.0-45-generic x86_64)
vagrant@vagrant:~$ singularity version
3.1.1-1
```
By default, Vagrant will share your project directory (the directory with the
Vagrantfile) to `/vagrant`. Inside the VM,
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

## Sylabs Cloud Services
With Sylabs Cloud services, one can push, share, sign and verify a container image.
To use these features with images, you must first generate an access token to
the Sylabs Cloud

1. Go to https://cloud.sylabs.io/
2. Click __Sign in to Sylabs__ and follow the sign in steps.
3. Click on your login id (same and updated button as the Sign in one).
4. Select __Access Tokens__ from the drop down menu.
5. Click the __Manage my API tokens__ button from the "Account Management" page.
6. Click __Create__.
7. Click __Copy token to Clipboard__ from the __New API Token__ page.
8. Paste the token string into your `~/.singularity/sylabs-token` file.
