Uninstall
=========

SureDrop is a containerised application composed of multiple services
deployed in a `docker
stack <https://docs.docker.com/v17.12/compose/bundles/>`_. A stack is a
collection of services that make up an application in a specific
environment. Uninstalling SureDrop is very easy and involves just the
following three steps:

-  First open a powershell admin console in your server.
-  Run the command :guilabel:`docker stack rm suredrop`. This will remove the
   ``suredrop`` stack. Services, networks, and secrets associated with
   the application will be removed.
-  Run the command :guilabel:`docker volume prune -f`. This will remove all
   local volumes not used by at least one container and the -f flag will
   suppress the prompt for confirmation.

That's it! It's simple, quick and effective.

.. Warning::
    Sometimes :guilabel:`docker volume prune -f` command doesn't delete
    anything or doesn't delete all volumes. That is because the volumes
    may still be marked as being used by some containers which haven't
    been removed yet. In this case, we either need to execute the volume
    prune command more than once, or run the command
    :guilabel:`docker container prune -f` followed by
    :guilabel:`docker volume prune -f`. Also remember that you can check if all
    volumes have been deleted or not using the command
    :guilabel:`docker volume ls`.

A typical example of this scenario could be something like this:

.. code:: sh

    D:\suredrop>docker stack rm suredrop
    Removing service suredrop_core
    Removing service suredrop_database-client
    Removing service suredrop_database-core
    Removing service suredrop_ngix-reverse-proxy
    Removing service suredrop_resources
    Removing service suredrop_rest-api
    Removing service suredrop_storage-server
    Removing service suredrop_storage-server-backup
    Removing network suredrop_webnet

    D:\suredrop>docker volume ls
    DRIVER              VOLUME NAME
    local               suredrop_core-shared
    local               suredrop_database-client-shared
    local               suredrop_database-core-shared
    local               suredrop_resources-shared
    local               suredrop_restapi-shared
    local               suredrop_storage-backup-shared
    local               suredrop_storage-primary-shared

    D:\suredrop>docker volume prune -f
    Total reclaimed space: 0B

    D:\suredrop>docker container prune -f
    Deleted Containers:
    3c48e80d3a64863e2c4f3d1d70eb502aea05d896df31865529d7a62aeb9805d2
    c97db5d1855f519ec8faf9ae1f6632a108797e6be505ce5957d313b6875cfad4

    Total reclaimed space: 0B

    D:\suredrop>docker volume prune -f
    Deleted Volumes:
    suredrop_database-core-shared
    suredrop_database-client-shared
    suredrop_restapi-shared
    suredrop_core-shared
    suredrop_resources-shared
    suredrop_storage-primary-shared
    suredrop_storage-backup-shared

    Total reclaimed space: 34.67MB

    D:\suredrop>docker volume ls
    DRIVER              VOLUME NAME

    D:\suredrop>

.. Note::
    Upon testing some more we've found that
    :guilabel:`docker system prune --volumes -f` is less flaky than
    :guilabel:`docker volume prune -f`. This is because it prunes the containers
    before calling prune on the volumes. So if you intend to go down
    this path, the uninstall is just a couple of commands:
    :guilabel:`docker stack rm suredrop` and
    :guilabel:`docker system prune --volumes -f`. Always remember to double
    check that the volumes have indeed been deleted with a
    :guilabel:`docker volume ls` command.
