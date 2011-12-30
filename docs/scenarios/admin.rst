Systems Administration
======================

Fabric
------

`Fabric <http://www.fabfile.org/>`_ is a command-line tool and a library
written in Python that allows a developer to automate various tasks, both
on the local machine and on remote servers. Fabric accomplishes this by
letting a developer execute arbitary shell commands on any number of
servers. Fabric tasks are pure Python, and can be organized, called and 
executed with full freedom that the Python language allows.

Most commonly, Fabric is used from the command line, in conjuntion with
a file of tasks, called a "fabfile". Assuming that all Fabric tasks are
specified in a ``fabfile.py`` file, here is how Fabric could be used to
deploy code to a remote server.

::
    
    # fabfile.py

    from fabric.api import env, local, run, put

    env.hosts = ['yourhost@yourdomain.com']
    env.user = 'your_admin_username'

    # Fabric will ask you for a password when it needs one, but using
    # a keyfile instead is a good idea.
    
    def upload():
        local('tar -czf ../yourapp.tgz *')
        put('../yourapp.tgz', '/var/www/apps')
        run('tar -xzf /var/www/apps/yourapp.tgz')

This Fabfile only defines a single task called ``upload``. On the local
machine, the developer can run ``fab upload`` and Fabric will find the
``fabfile.py`` file, look for a task called ``upload`` and execute it on
every server in the ``env`` variable. The task will be executed
sequentially on every server. This task will ``tar`` the folder locally,
``put`` (upload) the tar file to the remote server, and ``run`` the untar
command on the server. Subsequently, you can teach Fabric to restart the
server, download logs, run unit tests, etc. (Note that the user must be
in the same directory as the ``fabfile.py`` file to run ``fab``.)

Fabric is a simple tool, it's main purpose is to execute a simple set of
commands (upload a file, run a command remotely, run a command locally, etc)
so its usefulness depends entirely on the creativity of the developer. With
tools like error handling, grouping of servers by role and a simple API
Fabric becomes a great tool for automation.

The Fabric documentation lists several execution models and strategies that
explain more complication use-cases.

Chef
----

.. todo:: Write about Chef

Puppet
------

.. todo:: Write about Puppet

Blueprint
---------

.. todo:: Write about Blueprint

Buildout
--------

.. todo:: Write about Buildout
