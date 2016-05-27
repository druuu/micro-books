Basics
=========

Docker basics in simple words

1. Pull an Image to start with
2. Create a container
3. start, stop, rename, attach container
4. commit changes in container


1. Pull Docker Image
----------------------------

This is the first step as we need a virtual machine image to start with.

.. code-block:: python

    $ docker pull ubuntu

This command will pull ubuntu latest image from docker online repository.

You can see all images that you pulled with the following command

.. code-block:: python

    $ docker images


2. Working with Docker Containers
--------------------------------------

Now we should create container(s) from available docker images. Containers are like live os installed in a machine where are docker image is like OS DVD. We will install OS from DVD as we create container from Docker Image.

.. code-block:: python

    $ docker run ubuntu

This command will create and container from ubuntu image but it will not run as we didn't specify any parameters

.. code-block:: python

    $ docker run -itd ubuntu

The -itd stands for interactive terminal deamon.

.. code-block:: python

    $ docker ps

you can see running docker containers with this command

.. code-block:: python

    $ docker ps -l

you can see all container with this command, no matter if those are stopped or running.


3. start, stop, rename, attach container
--------------------------------------------

.. code-block:: python

    $ docker start <container_id>

This way you can start or stop containers.

Its good to rename container to remeber its purpose and you can do that with the following command

.. code-block:: python

    $ docker rename <old_container_name> <new_container_name>

.. code-block:: python

    $ docker attach <container_id>

This is the command to login to container, you can exit from container with normal 'exit' command but that will stop the container. Then you can start the container again.

You can take advantage of already running container by forking another process of bash and get a pseudo TTY by running:

.. code-block:: python

	docker exec -it <container ID> /bin/bash


4. commit changes in container
---------------------------------

You need to preserve changes made to the container to use at a later stage or to distribute to others.

.. code-block:: python

    $ docker commit -m "commit message" <container_id> name:tag

This will commit changes in the container and save it as an image to create containers.
