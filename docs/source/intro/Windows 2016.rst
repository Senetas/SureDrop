New Install - Windows 2016
==========================

.. Important::

   Please refer to the :doc:`What version to install<Version>` guide prior to 
   following the instructions below

Before starting this install you will need to contact sales and obtain
the following:

.. code:: sh

   a) Username
   b) Password
   c) Activation Key
   d) The Version of SureDrop to Install

Pre Requisites
--------------

#. Install :guilabel:`Windows Server 2016` with at **least** 12GB RAM and 100GB
   hard disk space.

(SET A STATIC IP!)


#. | Run MS update and install all updates.
   |  **(It's important that this step is done *before* step 3)**


#. **Reboot the server**


#. Install docker using an :guilabel:`admin powershell` with the following
   commands:

   .. code:: sh

      [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12

      Install-Module DockerMsftProvider -Force

      Install-Package Docker -ProviderName DockerMsftProvider -Force

   .. Note::

      If you see the following NuGet provider error message, press Y to install and continue

   .. code:: sh

      NuGet provider is required to continue PowerShellGet requires NuGet provider version '2.8.5.201' or 
      newer to interact with NuGet-based repositories. The NuGet provider must be available in 
      'C:\ProgramFiles\PackageManagement\ProviderAssemblies' or 
      'C:\Users\suredrop-admin\AppData\Local\PackageManagement\ProviderAssemblies'. 
      You can also install the NuGet provider by running 
      'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. 
      Do you want PowerShellGet to install and import the NuGet provider now?
      
      [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

   Also please have a look at our :doc:`Common configuration tasks`
   document for setting up proxy servers, virus scanners etc.


#. **Reboot the server again**





#. If you want to use remote SMB shares create two windows shares for storing the document data 
   (can be on the same server), and create an account that has full access to them:

   .. code:: sh

      \\[HOST-IP]\STORAGE01
      \\[HOST-IP]\STORAGE02

   .. Note:: 
    
      If you create these SMB shares on a different machine (within
      a domain) then please ensure that the user account has full access
      to them. An easy way to verify is to use the :guilabel:`net use` command
      with the user credentials. To give the appropriate access rights and
      to add them to the ACL list please right click on the folder and
      choose Properties. Then on Sharing tab click Advanced Sharing ->
      Permissions and add the user account with Full Control permissions
      and click OK. Then on the Security tab click Advance button and add
      the user with Full Control permissions on the folder , sub folders
      and files and click OK and finally click Apply and Close on the
      Properties window. Remember to give these permissions for both the
      primary and backup storage folders.


Installation of SureDrop
------------------------

#. Using an :guilabel:`admin powershell` run the following command:

   .. code:: sh

      wget "https://install.suredrop.com.au/create-suredrop.bat" -outfile "create-suredrop.bat";./create-suredrop.bat

   .. Note::
   
      This bat file will ask a series of questions and create the
      SureDrop instance. As part of this install an :guilabel:`answers.bat`
      file will be created in the same directory. Do not delete this
      file as it will be required to run an update if required, however
      please ensure the security on this file is locked down as this
      file contains secret information such as passwords in plain text.
      Ensure that there is one and only one ``admin powershell``
      window attempting the installation, multiple windows pointing to
      the install directory or storage locations will fail the
      installation. The install script is designed with defaults. Every
      feature is not relevant / required by all clients, so when not
      sure about any step it is wise to choose the default values.


#. Browse to the following url to complete the installation:

   .. code:: sh

      https://0-0-0-0.xip.suredrop.com.au

   For example if the IP address of this host is ``192.168.250.3``, then
   use ``https://192-168-250-3.xip.suredrop.com.au``. 
   
   .. Warning:

      Please wait until the CPU and disk usage drops to normalcy.


#. If everything is successful then the previous step should have opened
   the login page in your browser with 3 empty fields, company name,
   user name, and password. Please enter :guilabel:`SureDrop` in the first input
   box (for Company Name) and press tab or click on the next input box.
   This will take you to the create company page which allows the user
   to configure certain critical parameters of the system. The
   :guilabel:`Create Company` button is intentionally disabled at this stage.


#. Once you've filled the Activation Token from your SureDrop license
   certificate in the last input box of this page, then the
   :guilabel:`Create Company` button will be enabled and you should click on it.
   Once the company is created, SureDrop will automatically redirect you
   to the login page to create your ``administrator`` account password
   and then login to the system.


#. SureDrop should now be operational on your own compute
   infrastructure.

For any questions or if you have any issues following this document,
please email admin@suredrop.com.au.

.. _upgrade:

Upgrading or diagnosing a SureDrop instance
-------------------------------------------

#. Log onto the Windows 2016 Server running the SureDrop Docker
   Containers


#. Run an ``admin powershell`` and CD to the location where you placed
   the compose files and re-run the ``create-suredrop.bat`` file.

   .. code:: sh

      ./create-suredrop.bat


#. Choose option 1 for upgrading SureDrop to a version of your choice.


#. Choose option 4 for running diagnostics on SureDrop. See :doc:`Diagnostics`
   for details.


#. Choose option 5 for running a health check on SureDrop. See :doc:`Health check`
   for details.


Large File Support
------------------

*This only applies to :guilabel:`Download as Zip`, uploading and downloading of
individual files of any size is already supported by the default
configuration of SureDrop*

If you intend on downloading a large number of files using the
``Download as Zip`` option the following will need to be taken into
consideration.

#. The disk space on the docker host must be large enough to cater for
   3x the size of the zip file. For example, to download a zip file of
   1GB, there must be at least 3GB of available disk space on the
   application server.


#. If the zip file will be greater than 10GB, then large volume support
   will need to be enabled within the docker sub-system.


#. To enable large volume support create a file called
   ``update_docker_reg.reg`` and copy and paste the following into it:

   .. code:: sh

      Windows Registry Editor Version 5.00

      [HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Docker]
      "Type"=dword:00000010
      "Start"=dword:00000002
      "ErrorControl"=dword:00000001
      "ImagePath"=hex(2):22,00,43,00,3a,00,5c,00,50,00,72,00,6f,00,67,00,72,00,61,00,\
      6d,00,20,00,46,00,69,00,6c,00,65,00,73,00,5c,00,44,00,6f,00,63,00,6b,00,65,\
      00,72,00,5c,00,64,00,6f,00,63,00,6b,00,65,00,72,00,64,00,2e,00,65,00,78,00,\
      65,00,22,00,20,00,2d,00,2d,00,72,00,75,00,6e,00,2d,00,73,00,65,00,72,00,76,\
      00,69,00,63,00,65,00,20,00,2d,00,2d,00,73,00,74,00,6f,00,72,00,61,00,67,00,\
      65,00,2d,00,6f,00,70,00,74,00,20,00,73,00,69,00,7a,00,65,00,3d,00,31,00,36,\
      00,30,00,30,00,30,00,47,00,00,00
      "ObjectName"="LocalSystem"


#. Then double click on the file to edit the registry on the windows
   host.


#. Click on :guilabel:`Yes` in the following prompt.

   .. figure:: ../images/2.10.0/prompt1.png
      :alt: First prompt

#. Click on :guilabel:`OK` in the following dialog.

   .. figure:: ../images/2.10.0/prompt2.png
      :alt: Second prompt

#. **Restart the docker host**


Migrating the Database
----------------------

Most larger installs will want to migrate the client database from the
SQL Server Express version running in the ``database-client`` docker
container on the host.

The port ``14331`` has been left open for this purpose. Use SQL Server
Manager Studio 2016 to connect to the client instance and migrate the
suredrop client database to your own instance.

Once this has been done, use SQL Server Management Studio 2016 to
connect to the core database on port ``14330`` and update the table
``CoreConfigV2`` by setting the column ``sql_connection_string`` to the
new connection string for the relocated client database.
