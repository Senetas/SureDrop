Common configuration tasks
==========================

Disabling the Firewall
----------------------

Disable the firewall as it will interfere with connectivity to the docker containers.

In an :guilabel:`admin powershell` run the following command.

.. code:: sh

	Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled False

Disabling CPU Parking
---------------------

Disable CPU parking by running the following 2 commands.

.. code:: sh

    Powercfg -setacvalueindex scheme_current sub_processor CPMINCORES 100
    
    Powercfg -setactive scheme_current

Configuring a proxy server for Docker
-------------------------------------

To set proxy information for docker search and docker pull, create a
Windows environment variable with the name HTTP\_PROXY or HTTPS\_PROXY,
and a value of the proxy information. This can be completed with
PowerShell using a command similar to this:

.. code:: sh

    [Environment]::SetEnvironmentVariable("HTTP_PROXY", "http://username:password@proxy:port/", [EnvironmentVariableTarget]::Machine)

.. code:: sh

    Restart-Service docker

| For more information on configuring Docker, please visit `this webpage <https://docs.microsoft.com/en-us/virtualization/windowscontainers/manage-docker/configure-docker-daemon>`_


Setting Virus Scanners to Exclude the Docker Container Cache
------------------------------------------------------------

When running Docker on a host it is prudent to exclude the docker cache
location from real time scanning.

The default location is :guilabel:`C:\\ProgramData\\docker`

McAfee
~~~~~~

https://kc.mcafee.com/corporate/index?id=KB50998&page=content&pmv=print

Windows Defender
~~~~~~~~~~~~~~~~

https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-antivirus/configure-exclusions-windows-defender-antivirus

Trend Micro
~~~~~~~~~~~

https://success.trendmicro.com/solution/1059770-recommended-scan-exclusion-list-for-trend-micro-endpoint-products

AVG
~~~

https://support.avg.com/SupportArticleView?l=en&urlname=How-to-make-exclusions-from-all-scans-and-shields

Comodo
~~~~~~

https://help.comodo.com/topic-72-1-451-4758-.html

Norton
~~~~~~

https://support.norton.com/sp/en/au/home/current/solutions/v3672136_ns_retail_en_us
