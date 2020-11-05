Installing
==========

Versions
--------

**2.0.4** 

- Updated error message in logs to show when a key has not been encrypted with SKC

**2.0.3** 

- Fixed missing dependency

**2.0.2** (do not use)

- Updated xip certificate

**2.0.1** (do not use)

- Minor fixes for KeySecure (NextGen)

**2.0.0 Initial version**

- Configuration via the command prompt

- Standalone exe




Windows (x64)
------------- 

Version 2.0.4 https://skc-downloads.s3-ap-southeast-2.amazonaws.com/skc.2.0.4.win-x64.zip

Linux (Mainstream x64 distros)
------------------------------

Version 2.0.4 https://skc-downloads.s3-ap-southeast-2.amazonaws.com/skc.2.0.4.linux-x64.zip

Linux (Alpine and minimal distros)
----------------------------------

Version 2.0.4 https://skc-downloads.s3-ap-southeast-2.amazonaws.com/skc.2.0.4.linux-musl-x64.zip

Arm (Raspberry pi)
------------------

Version 2.0.4 https://skc-downloads.s3-ap-southeast-2.amazonaws.com/skc.2.0.4.linux-arm.zip

Arm (Linux distros)
-------------------

Version 2.0.4 https://skc-downloads.s3-ap-southeast-2.amazonaws.com/skc.2.0.4.linux-x64.zip

MacOS
-----

Version 2.0.4 https://skc-downloads.s3-ap-southeast-2.amazonaws.com/skc.2.0.4.osx-x64.zip

Unzip
-----

Unzip the zip file into any folder.

The structure should look like this:

.. code:: sh

	Install Location
	|
	+-- skc (skc.exe on windows)


Database Location
-----------------

SKC will automatically create an encrypted database required to store any persistent values, the location of this will be:

.. code:: sh

	C:\ProgramData\Senetas


On Linux it is located in the subdirectory of the current working folder called data:

.. code:: sh

	./data


