Install & Configure
=======================

Here we see installing Git in Ubuntu

.. code-block:: python

    $ sudo apt-get install git -y


**Git Configuration**

Git configuration can be of two types, global or local. 

* Global configuration is to identify user across all repositories in the computer/laptop. 
* Local configuration is to override global configuration and work with different user credentials for specific repositories.

*Global Configuration*

.. code-block:: python

    $ git config --global user.name "Your name"
    $ git config --global user.email your@email.com

*Local Configuration*

.. code-block:: python

    $ git config user.name "Your name"
    $ git config user.email your@email.com

