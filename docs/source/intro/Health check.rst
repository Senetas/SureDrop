Health check
============

In the SureDrop application server open an :guilabel:`admin powershell` console and browse to
the SureDrop install directory, then execute the

.. code:: sh

    wget "https://s3-ap-southeast-2.amazonaws.com/suredrop-downloads/compose/create-suredrop.bat" -outfile "create-suredrop.bat";./create-suredrop.bat

command. This will download the latest copy of the installer script from
the cloud and execute it. Now choose :guilabel:`5` to enter into the health
check mode.

.. code:: sh

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
    8) Schedule Automatic Updates

    9) Exit

    Enter number to select an option: 5

This script will then check

-  Docker service status
-  SureDrop docker container statuses
-  SureDrop core database docker container status
-  SureDrop client database docker container status
-  SureDrop core database status
-  SureDrop client database status
-  Primary storage status
-  Backup storage status

The expected output might look like this

.. code:: sh

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
    8) Schedule Automatic Updates

    9) Exit

    Enter number to select an option: 5

    Docker service status : RUNNING

    SureDrop containers:
    NAME                                CURRENT STATE           ERROR
    suredrop_storage-server.1           Running 5 minutes ago
    suredrop_storage-server-backup.1    Running 5 minutes ago
    suredrop_core.1                     Running 5 minutes ago
    suredrop_resources.1                Running 5 minutes ago
    suredrop_rest-api.1                 Running 5 minutes ago
    suredrop_ngix-reverse-proxy.1       Running 5 minutes ago
    suredrop_database-core.1            Running 5 minutes ago
    suredrop_database-client.1          Running 5 minutes ago

    SureDrop Core Database container status : Up 5 minutes

    SureDrop Client Database container status : Up 5 minutes

    SureDrop Core Database status : ONLINE

    SureDrop Client Database status : ONLINE

    Primary Storage Status: OK

    Backup storage verification: OK

If there are errors in any of these steps then SureDrop will not function correctly. 
So, please run the :doc:`Diagnostics` and contact the SureDrop support team immediately.
