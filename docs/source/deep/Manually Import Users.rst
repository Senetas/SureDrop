Manually Import Users
=====================

Users can now be manually imported to SureDrop via a delimited
comma-separated text (CSV) file. Manually importing user records enables
you to add numerous users in a single operation. Each line of the file
represents a user record. The first line of the file defines the field
headers. This functionality is available for **administrators and
forensic users** of the system. 

By default SureDrop will provide ``Standard`` role to every new user 
imported from the file. It will also send out an invitation email to 
the user with a link to activate his account. 

.. Warning::
   The users will be force created by default (i.e, any deactivated user 
   account with the same username will be overwritten).

Exporting users
---------------

Some identity providers such as Azure AD allows `downloading a list of
users <#https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/users-bulk-download>`_.
This import functionality in SureDrop was built for clients who cannot
integrate their AD servers to SureDrop but still want a bunch of users
to be added to the system.

How to import users in SureDrop
-------------------------------

1. Login to SureDrop and click on the Admin page on the top navigation
   bar.
2. Click on the ``Import Users`` button (right next to the
   ``Add New User`` button)
3. Select a CSV file with user records.

File structure
--------------

In the uncommon scenario when the SureDrop administrator wants to
manually create a CSV file, the file header must be
``userPrincipalName,displayName,surname,mail,givenName,mobile``.

-  **userPrincipalName** - this is the username used for logging into
   SureDrop.
-  **displayName** - this is the display name.
-  **surname** - this the user's surname.
-  **mail** - this is the email address.
-  **givenName** - a.k.a first name.
-  **mobile** - this the mobile number and must begin with a ``+``
   followed by the international calling code.

