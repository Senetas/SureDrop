Uninstall
=========

SureDrop is a containerised application composed of multiple services
deployed as `docker
containers <https://www.docker.com/resources/what-container>`_. 
Uninstalling SureDrop is very easy and can be done either using
``create-suredrop.bat`` script or ``suredrop.bat`` script. The former
uses ``suredrop.bat`` internally to perform the uninstall.

.. tabs::

   .. tab:: suredrop.bat

        -  First open a powershell admin console in your server.
        -  Browse to the SureDrop install directory.
        -  Run the command :guilabel:`./suredrop.bat stop`. This will remove the 
           services, networks, and secrets associated with the SureDrop application.
        -  Run the command :guilabel:`./suredrop.bat clean`. This will remove all
           persistent docker volumes and free up disk space.

   .. tab:: create-suredrop.bat

        -  First open a powershell admin console in your server.
        -  Browse to the SureDrop install directory.
        -  Run the command :guilabel:`./create-suredrop.bat`. This will display the
           SureDrop Configuration Menu. Enter ``9`` to uninstall SureDrop.

           .. code:: bash

              ******************************
              SureDrop Configuration
              ******************************
              1) Upgrade Version
              2) Upgrade PKI
              3) Upgrade Logging and Audit
              4) Diagnose
              5) Health check
              6) Add a Custom Root CA
              7) Restart Container Stack
              8) Start Container Stack
              9) Stop Container Stack
              10) Schedule Automatic Updates
              11) Exit

              Enter number to select an option: 9

.. Warning::

    ``suredrop.bat clean`` removes the persistent docker volumes and frees up
    disk space, however this action cannot be undone. If you want to **completely
    uninstall docker** from your system, then follow the `these instructions <https://docs.microsoft.com/en-us/virtualization/windowscontainers/manage-docker/configure-docker-daemon#how-to-uninstall-docker>`__.

That's it! It's simple, quick and effective.

.. Tip::

    After a complete uninstall always remember to double check that 
    the volumes have indeed been deleted with a :guilabel:`docker volume ls` 
    command. If they still exist then you will need to run the uninstall
    command again.
