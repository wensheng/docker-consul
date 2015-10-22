## prepare

use host IP 192.168.5.99 as an example.

make sure /etc/hosts, hostname, dig hostname, ping hostname all return correct answers

## install consul

    # from https://www.consul.io/downloads.html
    wget https://dl.bintray.com/mitchellh/consul/0.5.2_linux_amd64.zip
    sudo unzip 0.5.2_linux_amd64.zip -d /usr/local/bin/

## start consul

    consul agent -server -client=192.168.5.99 -bootstrap-expect 1 -data-dir /tmp/consul

## start registrator

    docker run -it -v /var/run/docker.sock:/tmp/docker.sock --net=host gliderlabs/registrator consul://192.168.5.99:8500

## start nginx consul template docker

    docker build -t my-nginx .  # use dockers/nginx-consul-template/Dockerfile
    docker run -it -e "CONSUL=192.168.5.99:8500" -e "SERVICE=simple" -p 80:80 my-nginx

## run service

    docker build -t python/server . # use dockers/python-server/Dockerfile
    docker run -it -e "SERVICE_NAME=simple" -p 8000:8000 python/server

we should be able to "lynx 192.168.5.99"

add another server for load balance:

    docker run -it -e "SERVICE_NAME=simple" -p 8001:8000 python/server

now "lynx 192.168.5.99" should load-balance


## references:

http://www.maori.geek.nz/scalable_architecture_dr_con_docker_registrator_consul_nginx/
