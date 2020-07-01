Diagnostics
===========

In the SureDrop application server open an :guilabel:`admin powershell` console and browse to
the SureDrop install directory, then execute the

.. code:: sh

    wget "https://s3-ap-southeast-2.amazonaws.com/suredrop-downloads/compose/create-suredrop.bat" -outfile "create-suredrop.bat";./create-suredrop.bat

command. This will download the latest copy of the installer script from
the cloud and execute it. Now choose :guilabel:`4` to enter into the diagnostics
mode.

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

    Enter number to select an option: 4

The script will then

-  get a list of all docker containers
-  try to get log files from all relevant containers
-  get a list of docker stacks
-  get a list of tasks within the SureDrop stack
-  verify database containers
-  gather system information

and finally generate a :guilabel:`diagnostics.txt` file (and an optional ``log``
directory). Please zip and send these files to the SureDrop support team
/ portal.
