KeySecure
=========

First configure KeySecure as follows by logging onto the KeySecure Web
Console:

Create a Key Server
-------------------

Click on the Device tab and make sure you have configured a Key Server
in ``Cryptographic Key Server Settings``.

The Key Server should be NAE-XML. Make sure you click on :guilabel:`Use SSL` and
supply a valid server certificate.

.. Warning::

    KeySecure can be configured to not use SSL, however it is not recommended.

Create a User
-------------

| Click on the :guilabel:`Security` tab at the top of the page and select :guilabel:`Local Authentication`
| Add a user and a password and select password expiration to ``none``

Create a Key
------------

| Click on :guilabel:`Managed Objects` > :guilabel:`Keys` > :guilabel:`Create Key`
| Enter the following:

| ``Key Name           = [any name]``
| ``Owner Username     = [the name of the user created above]``
| ``Algorithm          = [RSA-2048]``
| ``Activation Date    = [Immediately]``
| ``Process Start Date = [Immediately]``

In SureDrop
-----------

As ``Administrator`` in SureDrop, click on
:guilabel:`General Settings` > :guilabel:`Key Server Integration`

Enter the following:

| ``Key Server ID     = [any name]``
| ``Key Server Type   = Gemalto Key Secure``
| ``Key Server Location = [IPADDRESS:PORT[:tls]]``

.. code:: text

    nb. The :tls is optional and defines whether or not to use
    SSL for the connection to Key Secure.

    For Example:

    52-65-96-91.xip.suredrop.com.au:9000:tls

    IP   = 52-65-96-91.xip.suredrop.com.au
    PORT = 9000
    SSL  = tls

| ``Key Server Username = [user configured in KeySecure]``
| ``Key Server Password = [password for above user]``
| ``Key Name            = [The name of the key as configured in KeySecure]``

Click on the :guilabel:`Enable this Key Server` check box.

.. Note::
    The SSL configuration works with SureDrop version 2.4.1-final
    onwards.
