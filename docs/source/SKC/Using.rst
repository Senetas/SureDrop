Features 
========

The Senetas Key Orchestrator (SKC) is a REST API configured with a Swagger documentation server and xip (see below).

SKC currently uses basic authorization but has a roadmap to include Microsoft Active Directory and RADIUS authorization.  

SKC is designed to allow the two commands `encrypt` and `decrypt` to be accessible to standard developers for any data in a way that makes sense, is secure, is straight forward and doesn't mean you need a degree in encryption whilst still supporting enterprise HSM's such as SafeNet Luna HSM's, Thales KeySecure and key providers such as AWS KMS.
 

Documentation
=============

To view the Swagger documentation browse to the following location:

.. code:: sh

	http://localhost/swagger/v1
  
(or the local installed IP address)

The documentation at this point is brief however all API endpoints are shown.

Accessing
=========

The Key Orchestrator has an XIP certificate built in for TLS which can be accessed using the following format:

.. code:: sh

	https://127-0-0-1.xip.suredrop.com.au


Where 127-0-0-1 can be replaced the IP address where SKC is installed.

For example, if SKC was installed and was accessible at 1.1.1.1, you would be able to access SKC by using the following URL with a correctly validated certificate.

.. code:: sh

	https://1-1-1-1.xip.suredrop.com.au


For more information on how xip works please refer to:  

[XIP Readme](xip.io)   
[NIP Readme](nip.io)  

Unsealing
=========

Every time the SKC service is restarted the database is required to be unsealed before the service is available. 

There are two ways to unseal the SKC service:  

1. Run the skc executable with no parameters in interactive mode and select the unseal option in the menu.  

2. Make any API call to the REST API using the `admin` credentials.  

Authorization
=============

All authorization is done using HTTP basic authentication. Please pass the basic auth credentials with every API call.

API Call Format
===============

All REST API calls are done in JSON format with the exception of the following:  

Encrypt  
-------

.. code:: sh

	POST:/api/encrypt  
  

Encrypt will take the following formats:

application/json  
----------------

`Content-Type: application/json`
`Content-Type: application/json;charset=utf-8`  

The POST body must contain data in the following json format  

.. code:: sh

	{
	"plaintext":"[base64 encoded plaintext data]"
	}


or

.. code:: sh

	{
	"plaintext":"[plaintext data]"
	}


text/plain  
----------

`Content-Type: text/plain`
`Content-Type: text/plain;charset=utf-8`  

.. code:: sh

	[plaintext data]


application/base64  
------------------

`Content-Type: application/base64`
`Content-Type: application/base64;charset=utf-8`  

.. code:: sh

	[base64 plaintext data]
 

application/octet-stream  
------------------------

`Content-Type: application/octet-stream`

.. code:: sh

	[binary data]
 

Return Data
-----------

Encrypt returns data in the following format:

.. code:: sh

	{
	"ciphertext":"[base64 encoded ciphertext]"
	"status":"[ok]|[error]"
	}
  

Decrypt
-------

.. code:: sh

	POST:/api/decrypt  
 

Decrypt will take the following formats:

The POST body must contain the return data from the encrypt unmodified either as:  

.. code:: sh

	{
	"ciphertext":"[base64 encoded ciphertext]"
	"status":"ok"
	}
 

or

.. code:: sh

	[base64 encoded ciphertext]
 

Return Format
-------------


application/json  
----------------

`Content-Type: application/json`
`Content-Type: application/json;charset=utf-8`  

The data will be returned in the following format:  

.. code:: sh

	{
	"plaintext":"[base64 encoded plaintext data]",
	"status":"ok|error"
	"provider":"[provider id]"
	}


Where [provider id] is the id of the provider that supplied the KEK.



text/plain  
----------

`Content-Type: text/plain`
`Content-Type: text/plain;charset=utf-8`  

.. code:: sh

	[plaintext data]


application/base64  
------------------

`Content-Type: application/base64`
`Content-Type: application/base64;charset=utf-8`  

.. code:: sh

	[base64 plaintext data]
 

application/octet-stream  
------------------------

`Content-Type: application/octet-stream`

.. code:: sh

	[binary data]
 





 