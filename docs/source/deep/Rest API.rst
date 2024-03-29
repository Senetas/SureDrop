Rest API
========

This guide gives a quick start tutorial to using the REST API for
SureDrop.

Typically a development environment will be provided to the developer
that will either run on premises on a Windows Server 2016 host, or will
run in the cloud on a similar host. Please refer to the install
documentation to install a development version of SureDrop if you don't
already have a development environment set up.

The Development version of SureDrop uses Swagger to provide a self
documenting API for your use. To access the swagger documentation use
the following link:

.. code:: text

    https://[HOSTNAME]:[PORT]/api-docs

Where ``HOSTNAME`` is the name of the host where the development
SureDrop instance was installed, and ``[PORT]`` is the configured port,
by default the port is ``443``.

This document covers the following process:

As ``administrator``

1.  Initiate a new instance of SureDrop
2.  Get an 'auth token' for the default administrator account
3.  Create a new user
4.  Activate the new user and set a password
5.  Grant a read/write role to the new user
6.  Create a group
7.  Add the new user to the group

As ``new user`` (These steps can also be done as ``administrator``)

1.  Get a auth token for the new user
2.  Create a new folder in the group
3.  Upload a new file to that folder
4.  Get a list of groups of which the user is a member
5.  Get a list of folders in a group
6.  Get a list of files in a folder

.. raw:: html

   <hr>

Confirming a Successful Install
-------------------------------

To confirm that the development environment was installed successfully,
browse to the following location:

.. code:: text

    https://[HOSTNAME]:[PORT]/rest/ping

The return value should be:

.. code:: text

    STATUS 200
    {
      "ping":"pong"
    }

If you have followed the instructions for installing SureDrop, you will
have already initialized the master key and set an ``administrator``
password.

If this has not already been done, then this may be done
programatically. Please refer to the init section for details.

.. raw:: html

   <hr>

Init the SureDrop Instance
--------------------------

To init a fresh install development of SureDrop use the following REST
API calls:

.. code:: text

    POST https://[HOSTNAME]:[PORT]/rest/init?prefix=[COMPANY]

Where ``[COMPANY]`` is the name of the company that was used when
installing SureDrop

To set the ``administrator`` password use the following API call:

.. code:: text

    POST https://[HOSTNAME]/rest/password?prefix=[COMPANY]&username=administrator&two_factor=none
    {
     "password": "[PASSWORD]"
    }

Where ``[PASSWORD]`` is your new administrator password

.. raw:: html

   <hr>

Authorizing
-----------

To get an authorization token use the following REST API call:

.. code:: text

    GET:https://[HOSTNAME]:[PORT]/rest/session?prefix=[COMPANY]&username=administrator&password=[PASSWORD]&timeout=[TIMEOUT]

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[PASSWORD]`` = The password that was configured when the instance
   ``init`` was done
-  ``[TIMEOUT]`` = The number of ``minutes`` that the token will be
   valid for

This will return:

.. code:: text

    STATUS 200
    {
      "token":"XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
    }

OR

.. code:: text

    STATUS 200
    {
      "error":"[SOME ERROR]"
    }

Where:

-  ``XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX`` = the returned session
   token

-  ``[SOME ERROR]`` = the error returned from validating the username
   and password

.. raw:: html

   <hr>

Refreshing The Token (Optional)
-------------------------------

You reset the timeout on the token and at the same time test that the
token is valid by using the following REST API call:

.. code:: text

    GET https://[HOSTNAME]:[PORT]/rest/pinga/interval?prefix=[COMPANY]&username=administrator&token=[TOKEN]

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[TOKEN]`` = The token returned from an authorization call

This will return:

.. code:: text

    STATUS 200
    {
      "pinga":"ponga"
    }

OR

.. code:: text

    STATUS 200
    {
      "error":"[SOME ERROR]"
    }

.. raw:: html

   <hr>

Basic Administrator Commands
----------------------------

Creating a New User
~~~~~~~~~~~~~~~~~~~

To create a new user use the following REST API call:

.. code:: text

    POST https://[HOSTNAME]:[PORT]/rest/user?prefix=[COMPANY]&username=administrator&token=[TOKEN]
    {
     "first_name": "[FIRST]",
     "last_name": "[LAST]",
     "email": "[EMAIL]",
     "username": "[USERNAME]",
     "mobile": "[MOBILE]",
     "default_group": "_users"
    }

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[TOKEN]`` = The token returned from an authorization call
-  ``[FIRST]`` = The first name of the new user
-  ``[LAST]`` = The last name of the new user
-  ``[EMAIL]`` = The email address of the new user
-  ``[USERNAME]`` = By convention the ``[EMAIL]`` of the new user
-  ``[MOBILE]`` = Mobile number, if a mobile number is not supplied a
   ``+`` is required to be supplied in the field

This will return:

.. code:: text

    STATUS 200
    {
      "error":"noerror"
    }

OR

.. code:: text

    STATUS 200
    {
      "error":"[SOME ERROR]"
    }

Where:

-  ``[SOME ERROR]`` = the error returned

.. raw:: html

   <hr>

Activating a User
~~~~~~~~~~~~~~~~~

A user cannot be used until it has been activated. To activate a user
use the following REST API call:

.. code:: text

    POST https://[HOSTNAME]:[PORT]/rest/user/[USERNAME]/invite?prefix=[COMPANY]&username=administrator&token=[TOKEN]

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[TOKEN]`` = The token returned from an authorization call
-  ``[USERNAME]`` = The username of the newly created user that requires
   activation

This will return:

.. code:: text

    STATUS 200
    {
      "error":"noerror"
    }

OR

.. code:: text

    STATUS 200
    {
      "error":"[SOME ERROR]"
    }

This will result in an email being sent to the user with instructions on
how to activate their account.

Within this email will be the following link:

.. code:: text

    https://[HOSTNAME]:[PORT]/rest/certificate?username=[USERNAME]&token=[INVITETOKEN]&device=www&secure=no&format=html

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[INVITETOKEN]`` = A unique one time use token
-  ``[USERNAME]`` = The username of the newly created user that requires
   activation

To complete the activation the new user must click on this link. This
link will then redirect them to the login page of the SureDrop instance
where they will be able to set their password.

.. raw:: html

   <hr>

Adding a Role to a User
~~~~~~~~~~~~~~~~~~~~~~~

By default all new users are added with the ``Restricted`` role only,
which is the lowest permissions granted. The available roles that may be
granted are as follows. All Roles are calmative, in that each higher
role has all of the permissions granted to the lower roles plus the any
new permissions.

1. | Restricted
   | Read only within groups they have been added to.

2. | Standard
   | Read/Write within groups that they have been added to.

3. | Power
   | Ability to create groups and add existing users to a group that they either own or are a member of.

4. | Admin
   | Full access to all groups, not just those groups to which they are a member. Ability to invite new users to SureDrop.

5. | Forensic
   | Full forensic access to purged files.

To add a role to a user use the following REST API call:

.. code:: text

    POST https://[HOSTNAME]:[PORT]/rest/user/[USERNAME]/policy?prefix=[COMPANY]&username=administrator&token=[TOKEN]
    {
     "add": [
      "Standard User",
      "Power User",
      "Admin User",
      "Forensic User"
     ],
     "remove": []
    }

For example, to add just the ``Standard User`` role use the following
POST body:

.. code:: text

    {
     "add": [
      "Standard User"
     ],
     "remove": []
    }

For example, to remove the ``Standard User`` role use the following POST
body:

.. code:: text

    {
     "add": [
     ],
     "remove": [
        "Standard User"
     ]
    }

*nb. You will need to add at least ``Standard User`` if you wish to
upload documents to a group that the user is a member of*

.. raw:: html

   <hr>

Creating a Group
~~~~~~~~~~~~~~~~

Within SureDrop, users do not own files, groups own files and groups
have an assigned owner which may be changed at any time.

Before documents can be uploaded, a group must be created for storing
the documents.

To create a group use the following REST API call:

.. code:: text

    POST https://[HOSTNAME]:[PORT]/rest/group?prefix=[COMPANY]&username=administrator&token=[TOKEN]
    {
     "name": "[NEWGROUPNAME]",
     "storage": [
      "Backup",
      "Primary"
     ],
     "description": "[DESCRIPTION]"
    }

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[TOKEN]`` = The token returned from an authorization call
-  ``[NEWGROUPNAME]`` = The name of the new group
-  ``[DESCRIPTION]`` = The description of the group

This will return:

.. code:: text

    STATUS 200
    {
      "error":"noerror"
    }

OR

.. code:: text

    STATUS 200
    {
      "error":"[SOME ERROR]"
    }

.. raw:: html

   <hr>

Adding a User to an Existing Group
----------------------------------

Before the user can store files in a group they need to be added to the
group. This can be done using the folling REST API call:

.. code:: text

    POST https://[HOSTNAME]:[PORT]/rest/group/[GROUPNAME]/users?prefix=[COMPANY]&username=administrator&token=[TOKEN]
    {
     "add": [
      "[USERNAME]"
     ],
     "remove": []
    }

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[TOKEN]`` = The token returned from an authorization call
-  ``[GROUPNAME]`` = The name of the existing group that the user needs
   to be added to
-  ``[USERNAME]`` = The username of the user that needs to be added to
   the group

This will return:

.. code:: text

    STATUS 200
    {
      "error":"noerror"
    }

OR

.. code:: text

    STATUS 200
    {
      "error":"[SOME ERROR]"
    }

.. raw:: html

   <hr>

Basic User Commands
-------------------

Get a User Auth Token
---------------------

To get an authorization token use the following REST API call:

.. code:: text

    GET:https://[HOSTNAME]:[PORT]/rest/session?prefix=[COMPANY]&username=[USERNAME]&password=[PASSWORD]&timeout=[TIMEOUT]

Where:

-  ``[HOSTNAME]`` = HOst name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[USERNAME]`` = The username of the user that needs the token
-  ``[PASSWORD]`` = The password of the user
-  ``[TIMEOUT]`` = The number of ``minutes`` that the token will be
   valid for

This will return:

.. code:: text

    STATUS 200
    {
      "token":"XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
    }

OR

.. code:: text

    STATUS 200
    {
      "error":"[SOME ERROR]"
    }

.. raw:: html

   <hr>

Create a Folder
---------------

To create a folder use the following REST API call:

.. code:: text

    POST https://[HOSTNAME]:[PORT]/rest/folder/[GROUPNAME]/[NEWFOLDER]?prefix=[COMPANY]&username=[USERNAME]&token=[TOKEN]

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[USERNAME]`` = The username of the user that needs the token
-  ``[GROUPNAME]`` = The existing group
-  ``[TOKEN]`` = The token returned from an authorization call
-  ``[NEWFOLDER]`` = The name of the new folder, (sub folders are ok)

This will return:

.. code:: text

    STATUS 200
    {
      "error":"noerror"
    }

OR

.. code:: text

    STATUS 200
    {
      "error":"[SOME ERROR]"
    }

.. raw:: html

   <hr>

Upload a single file
--------------------

To upload a file use the following REST API call:

.. code:: text

    POST https://[HOSTNAME]:[PORT]/rest/document/[GROUPNAME]/[FOLDERNAME]/[FILENAME]?prefix=[COMPANY]&username=[USERNAME]&token=[TOKEN]&raw=raw

    [POST BODY]

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[USERNAME]`` = The username of the user that needs the token
-  ``[GROUPNAME]`` = The existing group
-  ``[FOLDERNAME]`` = The name of an existing folder, (sub folders are
   ok)
-  ``[FILENAME]`` = The name of the new file
-  ``[TOKEN]`` = The token returned from an authorization call
-  ``[POST BODY]`` = The binary file contents. If ``RAW`` is not set
   then the POST BODY is expected to be in multipart format.

.. raw:: html

   <hr>

Get a List of Groups
--------------------

To get a list of groups the user is a member of use the following REST
API call:

.. code:: text

    GET https://[HOSTNAME]:[PORT]/rest/groups?prefix=[COMPANY]&username=[USERNAME]&token=[TOKEN]&Role=[ROLE]

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[USERNAME]`` = The username of the user
-  ``[TOKEN]`` = The token returned from an authorization call
-  ``[ROLE]`` = ``Admin`` or ``Forensic`` or empty. Empty assumes that
   you only want the list of groups the user is a member of, even if the
   user is an administrator.

Returns (example data):

.. code:: text

    STATUS 200
    [
      {
        "group": "A New Group",
        "status": "ACTIVATED",
        "admin": "administrator",
        "description": "This is the description"
      },
      {
        "group": "administrators",
        "status": "ACTIVATED",
        "admin": "administrator",
        "description": ""
      }
    ]

Only ``ACTIVATED`` groups should be used, other statuses should be
ignored.

.. raw:: html

   <hr>

Get a List of Folders in a Group
--------------------------------

To get a list of folders in a group uses the following REST API call,
this call returns all of the folders and sub-folders in a group together
to allow for fast navigation within an app when navigating around
folders.

This is a *fast* and *lightweight* REST API call.

.. code:: text

    GET https://[HOSTNAME]:[PORT]/rest/folders/[GROUPNAME]?prefix=[COMPANY]&username=[USERNAME]&token=[TOKEN]

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[GROUPNAME]`` = The name of the group to get all of the folders and
   sub-folders in
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[USERNAME]`` = The username of the user
-  ``[TOKEN]`` = The token returned from an authorization call

Returns (example data):

.. code:: text

    STATUS 200
    [
      {
        "folder": "/A New Group",
        "deleted": "no"
      },
      {
        "folder": "/A New Group/A New Folder",
        "deleted": "no"
      },
      {
        "folder": "/A New Group/A New Folder/ONE",
        "deleted": "no"
      }
    ]

.. raw:: html

   <hr>

Get a List of Files in a folder
-------------------------------

Gets the list of files in a folder or sub-folder using the REST API:

.. code:: text

    GET https://[HOSTNAME]:[PORT]/rest/files/[GROUPNAME]/[FOLDERNAME]?prefix=[COMPANY]&username=[USERNAME]&token=[TOKEN]

Where:

-  ``[HOSTNAME]`` = Host name of the REST API
-  ``[PORT]`` = Port of the REST API (Generally 443)
-  ``[GROUPNAME]`` = The name of the group
-  ``[FOLDERNAME]`` = The name of the folder or sub-folder to get the
   files in
-  ``[COMPANY]`` = The company name that was configured on install
-  ``[USERNAME]`` = The username of the user
-  ``[TOKEN]`` = The token returned from an authorization call

Returns Example Data:

.. code:: text

    STATUS 200
    [
      {
        "url": "/A New Group/A New Folder/readme.md",
        "deleted": "no",
        "hash": "63D3D6C6925BE5B4DF6FFC82B4C934F55EA4BD07955B86CB7CEB100B3A55E598E5204DFF6E14981AB629FCA5BB5A7EEE",
        "size": "7845"
      },
      {
        "url": "/A New Group/A New Folder/readme.pdf",
        "deleted": "no",
        "hash": "975803EBD1BF94C3D443A957778CA30806D1FFC37BB9723C4EAEBB4036FEB348CC3B1CEEF3AD5B2B241E7BE74C53BCDB",
        "size": "107851"
      }
    ]

