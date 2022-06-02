Running
=======

Now that SKC has been configured you will need to run SKC as a service.

MacOS
-----

Under MacOS skc will need to be added as a daemon or added to the crontab as:

.. code:: sh

	@reboot /usr/local/bin/skc/skc -s public -d /usr/local/bin/skc  


Unix
----

Under Unix skc will need to be added as a daemon or added to the crontab as:

.. code:: sh

	@reboot /usr/local/bin/skc/skc -s public -d /usr/local/bin/skc  


Windows
-------

Under windows we have automatically added the capability to run skc as a service.

To install the service:
(As administrator)

.. code:: sh

	skc install -s public


To start the service:

.. code:: sh

	skc start

