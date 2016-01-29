
# Setting up a docker environment for 3-layer architecture



[Docker](https:/www.docker.com/) is becoming the new standard for packaging and delivering coud based web applications. 
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

