Running
=======

Now that SKC has been configured you will need to run SKC as a service. 
Some OS's restrict access to ports under 1024, so specifying the access port as 8443 
and the local managagemet port as 8080 resolves this issue. Do not specify these 
ports if you would use the the default ports of 443 for the access port and 80 for 
the locahost management port.

To get SKC specific help

.. code:: sh
	
	skc --help


MacOS
-----

Under MacOS skc will need to be added as a daemon or added to the crontab as:

.. code:: sh

	@reboot /usr/local/bin/skc/skc -s public -p 8443 -mp 8080 -db /usr/local/bin/skc  


Unix
----

Under Unix skc will need to be added as a daemon or added to the crontab as:

.. code:: sh

	@reboot /usr/local/bin/skc/skc -s public -p 8443 -mp 8080 -db /usr/local/bin/skc  


Windows
-------

Under windows we have automatically added the capability to run skc as a service.

To get windows service specific help

.. code:: sh

	skc help


To install the service:
(As administrator)

.. code:: sh

	skc install -s public -p 8443 -mp 8080


To start the service:

.. code:: sh

	skc start

