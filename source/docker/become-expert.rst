========================
Docker Advanced Commands
========================


To get list of all containers stopped/running
"""""""""""""""""""""""""""""""""""""""""""""

.. code-block:: shell
    
   docker rm $(docker ps -aq)

To remove all stopped containers
""""""""""""""""""""""""""""""""

.. code-block:: shell
    
   docker rm $(docker ps -aq)

It is safe to run this command because it will delete all the stopped container and running containers, since they are not stopped will throw an error.

To get detailed information about docker container
""""""""""""""""""""""""""""""""""""""""""""""""""

.. code-block:: shell
    
   docker inspect <container-name/id>




=================
Using Dockerfile:
=================

When you want to modify an existing image, you can do it using Dockerfile.
Say you want to install a package in container or if you will Destroy the image,
but want to be able to build it anytime. preparing a Dockerfile can help you in
building an image anytime.

**Basic Dockerfile to install a package:**

.. code-block:: shell

  FROM ubuntu:14.04
  MAINTAINER jagadeesh@micropyramid.com
  RUN apt-get update && apt-get -y install nginx

The above command will download/use Ubuntu 14.04 image and updates and installs nginx.

**Note: This is for reference purpose only, You can also use nginx docker image.**

**Building the Image out of Dockerfile:**

.. code-block:: shell

  docker build -t <image-name>:<image-tag> .


**Other Important Commands:**

.. code-block:: shell

    COPY <source> <destination> - to copy files into a docker container
    EXPOSE <source-port>:<destination-port> - binds the source port to docker container port.
    CMD <command>  -  to run a command in container shell.
    VOLUME ["<volume-here>"] - to mount an directory into docker file
    ENV <key> <value> - to use in docker file.
    WORKDIR <dir-path>    - to set workng directory for the commands that follow next.
    ENTRYPOINT - to run few commands while starting a container.
    

===============================
Persisting the container state:
===============================

**Use Case:**

The above image you prepared when you run it will install nginx but to keep the container in running state, eventhough you add ENTRYPOINT as sudo service nginx start. The Docker container will close because its done executing the ENTRYPOINT/commands in file. So you need to apply a small hack.

.. code-block:: shell

  #!/bin/sh

  sudo service nginx start
  /bin/bash

Now give it executive permissions.

.. code-block:: shell

  FROM ubuntu:14.04
  MAINTAINER jagadeesh@micropyramid.com
  RUN apt-get update && apt-get install nginx
  COPY docker-entrypoint.sh /root
  ENTRYPOINT ["/root/docker-entrypoint.sh"]

run it using


.. code-block:: shell

    docker run -itd <image-name>

This is only a small hack to keep container in running state.
The /bin/bash will start a terminal session without closing it after starting nginx

=====================
Networking in Docker:
=====================

By default docker will create network with ip Series 172.17.x.x but you can also
start different networks and assign them to docker containers accordingly.

**To check Networks:**

.. code-block:: shell

    docker network ls
    docker network inspect <network-name>


**To start a new network:**

.. code-block:: shell

    docker network create --driver bridge <network-name>

This will also start a new docker network with 172.x.x.x, you can maintain seperate networks in case if you want your containers isolated from others

**To attach docker container to network:**

.. code-block:: shell

    docker run <image-name>  --net=<network-name>

