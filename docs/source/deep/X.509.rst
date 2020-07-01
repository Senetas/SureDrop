X.509 Certificates
==================

X.509 certificates are used to provide encryption and identification of
communication between two end points.

.. Note::

    An X.509 certificate contains a public key and an identity 
    (a hostname, or an organization, or an individual), and is either 
    signed by a certificate authority or self-signed. 
    
    - Wikipedia


When the X.509 certificate is signed by a certificate authority which is
known and trusted, it is said that the Certificate Chain has been
validated.

Certificate Chains
------------------

.. Note::

    A certificate chain (see the equivalent concept of "certification path" defined by 
    RFC 5280)[10] is a list of certificates (usually starting with an end-entity certificate) 
    followed by one or more CA certificates (usually the last one being a self-signed certificate), 
    with the following properties:

    1. The Issuer of each certificate (except the last one) matches the 
       Subject of the next certificate in the list.

    2. Each certificate (except the last one) is supposed to be signed by 
       the secret key corresponding to the next certificate in the chain 
       (i.e. the signature of one certificate can be verified using the 
       public key contained in the following certificate).

    3. The last certificate in the list is a trust anchor: a certificate that 
    you trust because it was delivered to you by some trustworthy procedure. 
    
    - Wikipedia

TLS Encryption
--------------

TLS encryption relies on valid X.509 certificates to not only provide
encryption, but to also guarantee the identity of the party at the other
end.

Within SureDrop TLS is used to secure the connection to the main
SureDrop application server as well as to secure any connections to
external services such as KeySecure.

Weaknesses
----------

There are a number of weaknesses in this architecture, however a
fundamental weakness is that it is not possible to currently issue an
X.509 certificate where the Common Name refers to an internal, non
routable IP address.

In fact any such request should be denied by all certificate
authorities.

An X.509 certificate may be issued to a DNS in which it's A record
points to an internal non-routable IP address however.

This effectively means that when securing internal connections using TLS
between internal IP addresses, only self signed certificates or
certificates issued from an internal Certificate Authority can be used
unless a DNS resolves a valid DNS name to an internal IP.

A self signed certificate may be used, however, this requires that the
Root Certificate of the internal Certificate Authority must be added to
the list of trusted root certificates in the stack of the client.

In the case of SureDrop, this would require the root certificate to be
somehow added to the trusted certificate store of the main rest-api
windows container, a difficult task.

The Problem
-----------

So in summary, the problem is that it is currently difficult to secure
connections between SureDrop and clients and between SureDrop and
KeySecure using TLS when using internal non-routable IP addresses.

The two suggested solutions are:

1. Use valid DNS names to point to internal IP addresses and purchase
   public X.509 certificates from a trusted Certificate Authority.

2. Use an internal CA

.. code:: text

   Neither of these two solutions are appropriate for proof of concept, 
   trial or initial installs of SureDrop

The solution
------------

The solution is to use a loose standard called ``xip.io``

(Please take a moment to look at this website)

<https://sslip.io>

Using this standard and a custom DNS server, it is possible to create
custom DNS names which resolve dynamically.

For example:

.. code:: text

    10-0-0-1.xip.suredrop.com.au      resolves to   10.0.0.1
    192-168-0-1.xip.suredrop.com.au   resolves to   192.168.0.1

*Senetas manage and maintain this custom DNS server at
``.xip.suredrop.com.au``*

In conjunction to this, Senetas have requested an X.509 certificate from
a trusted Certificate Authority for the following Common Name:

.. code:: text

    *.xip.suredrop.com.au  

    Issued by: COMODO RSA Domain Validation Secure Server CA
    Expires: Saturday, 29 August 2020 at 9:59:59 am Australian Eastern Standard Time
    PositiveSSL Wildcard

By default we ship this certificate in the SureDrop application server.
This is the certificate which is used to encrypt TLS traffic by default
in the containerized version of SureDrop.

After spinning up SureDrop on a Windows instance you will be asked to
connect using the following format URL:

``https://0-0-0-0.xip.suredrop.com.au``

Where ``0-0-0-0`` is the IP address of the windows server instance with
the ``.`` replaced by ``-``

*Because the DNS matches the Common Name in the X.509 certificate, the
certificate is valid.*

.. Tip::
   What we are doing here is removing the Identity component 
   to facilitate TLS as we are connecting to an internal IP address on our own 
   network. For production instances which are accessed externally it is 
   recommended that a reverse proxy be put in place with a valid public certificate 
   which is restricted to one common name.

KeySecure
---------

For connecting to KeySecure we are able to provide the
\*.xip.suredrop.com.au certificate and private key on request for
loading into KeySecure.

This allows encrypted TLS traffic between SureDrop and KeySecure, even
on internal networks.
