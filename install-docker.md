## Install docker

    sudo apt-get install linux-image-generic-lts-trusty

reboot

    sudo apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    sudo vi /etc/apt/sources.list.d/docker.list # add following

for Ubuntu Precise

    deb https://apt.dockerproject.org/repo ubuntu-precise main

for Ubuntu Trusty

    deb https://apt.dockerproject.org/repo ubuntu-trusty main

    sudo apt-get update
    sudo apt-cache policy docker-engine
    sudo apt-get install docker-engine

## Test docker installation

    sudo docker run hello-world

## docker without sudo

    sudo usermod -aG docker wensheng

logout and log back in:

    docker run hello-world
    docker run -it ubuntu bash
