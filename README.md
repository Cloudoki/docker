
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

### [docker-machine](https://docs.docker.com/machine/)

`docker-machine` will install the old boot2docker ISO in a VirtualBox VM. The boot2docker.iso image contains a lightweight linux distribution based on [Tiny Core Linux](http://tinycorelinux.net)  and [BusyBox](https://www.busybox.net).


`docker-machine` is meant to run on the OS X host and provides a user friendly interface to managing docker VMs.


`docker-machine help` will give a list of commands that will allow the complete management of the docker VMs installed in your system. 

Lets get quickly setup with a docker machine.

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

Note that the last line of the output there suggests running `docker-machine env`. We'll be using that a lot, especially when managing multiple machines.

If we run `docker-machine ls` again we'll see the newly created machine

    $ docker-machine ls
    NAME       ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER   ERRORS
    cloudoki   -        virtualbox   Running   tcp://192.168.99.102:2376           v1.9.1
    $

At this point the machine is not active which means that when running `docker ps` docker will complain that it can't find the docker daemon.

Lets look at the `docker-machine env` output:

    $ docker-machine env cloudoki
    export DOCKER_TLS_VERIFY="1"
    export DOCKER_HOST="tcp://192.168.99.102:2376"
    export DOCKER_CERT_PATH="/Users/csouza/.docker/machine/machines/cloudoki"
    export DOCKER_MACHINE_NAME="cloudoki"
    # Run this command to configure your shell:
    # eval $(docker-machine env cloudoki)
    $

This will display the docker environment variables needed for docker to connect to the machine. You can add those to your `.bash_profile` if you know that you will be using a single docker machine instance
but its better to configure the shell dynamically with `eval $(docker-machine env cloudoki)`. You can unset any variables later with  `eval $(docker-machine env -u)`

    $ eval $(docker-machine env cloudoki)
    $ export -p | grep -i docker
    declare -x DOCKER_CERT_PATH="/Users/cloudoki/.docker/machine/machines/cloudoki"
    declare -x DOCKER_HOST="tcp://192.168.99.102:2376"
    declare -x DOCKER_MACHINE_NAME="cloudoki"
    declare -x DOCKER_TLS_VERIFY="1"
    $ eval $(docker-machine env -u)
    $ export -p | grep -i docker
    $

So lets then activate this machine 

    $ eval $(docker-machine env cloudoki)
    $ docker-machine ls
    NAME       ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER   ERRORS
    cloudoki   *        virtualbox   Running   tcp://192.168.99.102:2376           v1.9.1
    $

`docker-machine` has many commands to manage the VM. The most common are `docker-machine ls`,  `docker-machine env`, `docker-machine start`, `docker-machine stop` and `docker-machine restart`


Other commands are:

```
  active		Print which machine is active
  config		Print the connection config for machine
  create		Create a machine
  env			Display the commands to set up the environment for the Docker client
  inspect		Inspect information about a machine
  ip			Get the IP address of a machine
  kill			Kill a machine
  ls			List machines
  regenerate-certs	Regenerate TLS Certificates for a machine
  restart		Restart a machine
  rm			Remove a machine
  ssh			Log into or run a command on a machine with SSH.
  scp			Copy files between machines
  start			Start a machine
  status		Get the status of a machine
  stop			Stop a machine
  upgrade		Upgrade a machine to the latest version of Docker
  url			Get the URL of a machine
  version		Show the Docker Machine version or a machine docker version
  help			Shows a list of commands or help for one command
```

Now that we have a docker environment set up, lets install some containers


