Providers
=========

Providers are plug in services that provide encryption/decryption of the keys used for encrypting data. Several providers are already provisioned.  

*Providers contain the master keys which are never made visible to either the Key Orchestrator or an end user*


Amazon AWS Key Management Service (KMS)  
---------------------------------------

Amazon KMS provides key management as a SaaS solution.  

Amazon AWS KMS https://github.com/Senetas/SKC/wiki/Configuring-an-AWS-KMS-provider


Thales KeySecure (Classic & Nexgen)  
-----------------------------------

Both Key Secure Classic and NextGen are both supported via the NAE-XML interface provided by both.

Thales SafeNet Luna HSM  
-----------------------

The Thales SafeNet HSM is supported via the KSP encryption service provided by Microsoft.
(Supported only under the Windows version of SKC)  

Thales SafeNet Luna HSM Provider https://github.com/Senetas/SKC/wiki/Configuring-a-Thales-SafeNet-Luna-HSM-Provider


 
Senetas KeyVault  
----------------

The Key Vault is a Senetas High Speed Encryptor (HSE) with additional API's to enable encryption/decryption and provision of quantum generated key material via the IDQ Quantis Quantum Random Number Generator.  

Senetas Key Orchestrator (SKC)  
------------------------------

SKC can also be used as a remote provider