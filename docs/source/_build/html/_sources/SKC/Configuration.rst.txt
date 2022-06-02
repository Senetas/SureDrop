Configuration  
=============

When SKC is running interactively it does not require that the service is running to add/edit/delete keys, providers or users. SKC accesses the encrypted database directly. If SKC is also running as a service then the interactive instance will ensure that the cache has been flushed on the service each time an add/edit/delete is performed on the database to ensure consistency.  

Before we can use SKC we need to configure at least one Key Management Solution (KMS) provider at a minimum.  A provider provides a Key Encryption Key (KEK) to ensure that the Data Encryption Key (DEK) is encrypted appropriately.  

As an example we will show how to configure SKC using an Amazon KMS provider.  

First follow these instructions for creating an AWS KMS key.

[Configuring an AWS KMS provider](https://github.com/Senetas/SKC/wiki/Configuring-an-AWS-KMS-provider)  

You will need to remember the following pieces of information:

1. The region you created the key in
2. The AWS Key
3. The AWS Secret
4. The Key ID 

.. figure:: https://user-images.githubusercontent.com/457335/82018257-4399cd00-96c8-11ea-9d9c-8204ec292f21.png  

First select `3. Manage` -> `3. Providers` -> `2. Add` -> `1. Add AWS KMS`  

.. figure:: https://user-images.githubusercontent.com/457335/82018520-d2a6e500-96c8-11ea-9d34-1db0ee2ee5dc.png

Add an ID for your provider. This must be unique to this provider.  

.. figure:: https://user-images.githubusercontent.com/457335/82018596-f5d19480-96c8-11ea-9b21-c6be589ac7f3.png

Add a description.  

.. figure:: https://user-images.githubusercontent.com/457335/82018657-17328080-96c9-11ea-809b-e7ee37feff78.png

Select the region the key was created in. A list of regions and their names are: 

.. code:: sh

	US East (Ohio)                    us-east-2
	US East (N. Virginia)             us-east-1
	US West (N. California)           us-west-1
	US West (Oregon)                  us-west-2
	Africa (Cape Town)                af-south-1
	Asia Pacific (Hong Kong)          ap-east-1
	Asia Pacific (Mumbai)             ap-south-1
	Asia Pacific (Osaka-Local)        ap-northeast-3
	Asia Pacific (Seoul)              ap-northeast-2
	Asia Pacific (Singapore)          ap-southeast-1
	Asia Pacific (Sydney)             ap-southeast-2
	Asia Pacific (Tokyo)              ap-northeast-1
	Canada (Central)                  ca-central-1
	China (Beijing)                   cn-north-1
	China (Ningxia)                   cn-northwest-1
	Europe (Frankfurt)                eu-central-1
	Europe (Ireland)                  eu-west-1
	Europe (London)                   eu-west-2
	Europe (Milan)                    eu-south-1
	Europe (Paris)                    eu-west-3
	Europe (Stockholm)                eu-north-1
	Middle East (Bahrain)             me-south-1
	South America (São Paulo)         sa-east-1



.. figure:: https://user-images.githubusercontent.com/457335/82019265-41387280-96ca-11ea-9770-4aa3051a8a9e.png

Enter the AWS Account Key  

.. figure:: https://user-images.githubusercontent.com/457335/82019328-61683180-96ca-11ea-8767-7713c231e6bc.png

Enter the AWS Account secret  

.. figure:: https://user-images.githubusercontent.com/457335/82019501-b015cb80-96ca-11ea-993b-b17b8b9a898e.png  

Enter the priority of this provider.

.. figure:: https://user-images.githubusercontent.com/457335/82019634-efdcb300-96ca-11ea-9161-6af95ac09881.png  

Enter the default KMS Key ID.  This is the key that is used by default for all encrypt requests to this provider unless a specific key name is provided for the encrypt operation.  

.. figure:: https://user-images.githubusercontent.com/457335/82019915-67aadd80-96cb-11ea-9a07-f99cd5522d37.png  

Multiple key alias mappings can be done to map a key alias to a key ID, however, only one is required.  

.. figure:: https://user-images.githubusercontent.com/457335/82020031-ab9de280-96cb-11ea-960a-3ce18585efef.png  

Optional arbitrary `Tags` may be entered as extra metadata at this point.  

.. figure:: https://user-images.githubusercontent.com/457335/82020240-13542d80-96cc-11ea-8f01-663362f4e842.png  

If all of these details are correct select `1. True`.  

SKC is now configured with the minimum of 1 provider!  