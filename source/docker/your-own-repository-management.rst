
===============
Docker Registry: 
================

Docker Registry is a Open Source application that stores and ditributes images from your on-premise server.

=================
SSL certificates:
=================

We use letsencrypt to generate the certificates. After Generation of SSL certifiates their location will be /etc/letsencrypt/live/<domain-name>. rename fullchain.pem and privkey.pem to fullchain.crt and privkey.key respectively 

=========
Registry:
=========

Docker Command to run a registry server is


.. code-block:: bash

    docker run -d -p 443:5000 --restart=always --name registry -v /etc/letsencrypt/live/<domain-name>:/certs -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/fullchain.crt -e REGISTRY_HTTP_TLS_KEY=/certs/privkey.key registry:2

This will download and start a docker container running docker registry server.

Assume our server DNS is example.com

After launching docker container, accessing https://example.com/v1 will return STATUS 200.

If you have already have a image tag it as example.com/<repo-name>:<tag-name>


.. code-block:: bash

    docker push example.com/<repo-name>:<tag-name>
    docker pull example.com/repo-name>:<tag-name>

Accessing it through UI:
""""""""""""""""""""""""

To access it through UI you will need web application. There are already pre-defined docker images which can do that hyper/docker-registry-web

.. code-block:: bash

    docker run -itd --restart=always -p 80:8080 --link registry -e REGISTRY_HOST=<domain-name> -e REGISTRY_PORT=443 hyper/docker-registry-web

Now we can manage repositories from Web Interface

**Note:**

For Secuirty, you can either use firewall to Restrict IPS or create a authentication and authorization to application.

