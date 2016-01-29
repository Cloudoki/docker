
# Setting up a docker environment for 3-layer architecture



[Docker](https:/www.docker.com/) is becoming the new standard for packaging and delivering cloud based web applications. 
It is natively supported on Linux and on other operating systems within a virtual machine environment.

It is supported by the following services:

- Amazon Web Services
- Microsoft Azure
- Digital Ocean
- Exoscale
- Google Compute Engine
- Generic
- Microsoft Hyper-V
- OpenStack
- Rackspace
- IBM Softlayer
- Oracle VirtualBox
- VMware vCloud Air
- VMware Fusion
- VMware vSphere

On MacOS X docker runs in a virtual machine using Oracle VirtualBox or VMware and even Parallels. 

MacOS X with homebrew and VirtualBox will be assumed for the rest of this readme.


## Installation

Install everything with homebrew `brew install docker docker-machine docker-compose`

### docker-machine 

`docker-machine` will install the old boot2docker ISO in a VirtualBox VM. The boot2docker.iso image contains a lightweight linux distribution based on [Tiny Core Linux](http://tinycorelinux.net)  and [BusyBox](https://www.busybox.net).


`docker-machine` is meant to run on the OS X host and provides a user friendly interface to managing docker VMs.


`docker-machine help` will give a list of commands that will allow the complete management of the docker VMs installed in your system. 

Lets get quickly setup with two docker machines.

`docker-machine ls` will list any installed machines. We currently don't have any:

    $ docker-machine ls
    NAME   ACTIVE   DRIVER   STATE   URL   SWARM   DOCKER   ERRORS
    $

We'll install our first machine using `docker-machine create --driver=virtualbox <name>`

    $ docker-machine create --driver=virtualbox cloudoki
    Running pre-create checks...
    Creating machine...
    (cloudoki) Copying /Users/cloudoki/.docker/machine/cache/boot2docker.iso to /Users/cloudoki/.docker/machine/machines/cloudoki/boot2docker.iso...
    (cloudoki) Creating VirtualBox VM...
    (cloudoki) Creating SSH key...
    (cloudoki) Starting VM...
    Waiting for machine to be running, this may take a few minutes...
    Machine is running, waiting for SSH to be available...
    Detecting operating system of created instance...
    Detecting the provisioner...
    Provisioning with boot2docker...
    Copying certs to the local machine directory...
    Copying certs to the remote machine...
    Setting Docker configuration on the remote daemon...
    Checking connection to Docker...
    Docker is up and running!
    To see how to connect Docker to this machine, run: docker-machine env cloudoki
    $
