New Install - Virtual Machine
==========================================

Before starting this install you will need to contact support and obtain
the following:

   * Username
   * Password
   * Activation Key
   * The Version of SureDrop to Install
   * A share pointing to the location of the Virtual Box appliance
   * The password for the appliance

.. admonition:: Prefer watching over reading?

   Check out `this <https://youtu.be/iymHek_5MPU>`_ screencast video.
   
   .. raw:: html
   
       <div style="text-align: center; margin-bottom: 2em;">
       <iframe width="100%" height="350" src="https://www.youtube.com/embed/iymHek_5MPU" frameborder="0" allow="autoplay; encrypted-media;" allowfullscreen></iframe>

       </div>


#. Download the Virtual Box Appliance from the share provided.

	**This appliance is an .ova file about 13Gb in size**

#. While the ova is downloading install Oracle Virtual Box from the following location.

	.. code:: sh

	 https://www.virtualbox.org/wiki/Downloads
		
#. After you have installed Virtual Box and downloaded the .ova file, import the appliance.

	.. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-5.39.37-pm.png

	.. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-5.41.15-pm.png

	.. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-5.50.54-pm.png

	.. hint::

		Remember to change the name to something that you recognize


	**This should take about 10 minutes to import**

#. Once is has imported run the new virtual Machine

	.. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-6.01.54-pm.png

	.. note::

	You will need the password to log in provided by the SureDrop team

#. Run the ``Configure SureDrop`` application on the desktop.

	.. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-6.06.16-pm.png

	.. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-6.07.56-pm.png

#. ``Stop`` the Processes if they are ``Running...`` 

#. Enter the information into the top four fields that was provided on your license certificate and click on ``Save``

#. Confirm that the IP address is correct, if it is not then check ``Manual`` and enter the correct IP address of the VM.

#. Click on the ``Check For Updates``.

	.. warning::

	 This may take up to an hour.

	.. hint::

	 If you want to see the progress of this command run a ``cmd prompt`` and run the following command:

	 c:\\Users\\Administrator>suredrop get

	.. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-6.16.33-pm.png
	
#. Click on ``Start``

#. Browse to the url displayed at the bottom of the application

   .. code:: sh

      https://XXX-XXX-XXX-XXX.xip.suredrop.com.au

   For example if the IP address of this host is ``192.168.250.3``, then
   use the following:

   .. code:: sh

      https://192-168-250-3.xip.suredrop.com.au


#. If everything is successful then the previous step should have opened
   the login page in your browser with 3 empty fields, company name,
   user name, and password. 
   
   .. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-4.15.39-pm.png
   
   
#. Enter **SureDrop** in the first input box
   (for Company Name) and press tab or click on the next input box. 
   
   .. note::
		The initial company name is SureDrop

   This will take you to the create company page which allows the user to
   configure certain critical parameters of the system. The Create
   Company button is intentionally disabled at this stage.


	.. Hint::

		You may need to wait a few seconds for the create company page to appear

	.. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-5.02.50-pm.png


#. Once you've filled the Activation Token from your SureDrop license
   certificate in the last input box of this page, then the Create
   Company button will be enabled and you should click on it. Once the
   company is created, SureDrop will automatically redirect you to the
   login page to create your administrator account password and then
   login to the system.

	.. figure:: ../images/2.10.0/Screen-Shot-2020-06-16-at-5.05.41-pm.png


#. SureDrop should now be operational on your own compute
   infrastructure.

For any questions or if you have any issues following this document,
please email admin@suredrop.com.au.








	
