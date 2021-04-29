SureDrop Documentation
======================

`SureDrop <https://www.sdrop.com>`_ is a secure file sharing and collaboration tool that is similar in function to DropBox, 
Box or Google Drive but with several important security and usability benefits. It is a simple, secure 
& convenient place to store files and allows users to easily collaborate and share with each other.

..  important::

    Maintaining good quality documentation is a priority for SureDrop. 
    If you find missing or inaccurate content, or if you'd like to extend 
    the wiki with a topic or tutorial, or have questions please click on 
    the ``Edit on GitHub`` link on the top of the page and let us know via 
    the issue tracker.

SureDrop was designed from the ground up with security front of mind, security features include a fully 
encrypted and authenticated storage environment, support for 2FA, integrations with Thales' best in class 
key management solutions, flexible deployment options either on premises or in public / private cloud environments, 
role-based user management and integrations with Active Directory.

Here you will find **all technical information** including release notes, installation and integration guides, 
FAQs, etc. about SureDrop.

`This <https://youtu.be/3pwnRjww8Vg>`_ screencast video will help you get started.

.. raw:: html

    <div style="text-align: center; margin-bottom: 2em;">
    <iframe width="100%" height="350" src="https://www.youtube.com/embed/3pwnRjww8Vg?rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
    </div>


.. toctree::
   :maxdepth: 2
   :caption: Getting Started
   :hidden:

   /intro/Version
   /intro/Common configuration tasks
   /intro/Windows 2016
   /intro/Windows 2019
   /intro/SureDropVm
   /intro/Create-cloud-login
   /intro/Uninstall
   /intro/Diagnostics
   /intro/Health check

.. toctree::
   :maxdepth: 2
   :caption: Integrations
   :glob:
   :hidden:

   /integrations/*

.. toctree::
   :maxdepth: 2
   :caption: Senetas Key Orchestrator
   :glob:
   :hidden:

   /SKC/Overview
   /SKC/Installing
   /SKC/Running
   /SKC/Configuration
   /SKC/Providers
   /SKC/Using
   /SKC/Suredrop Integration

.. toctree::
   :maxdepth: 2
   :caption: Digging Deeper
   :hidden:

   /deep/SureDrop-Architectures
   /deep/Azure Architecture
   /deep/Rest API
   /deep/Roles
   /deep/Manually Import Users
   /deep/Backup
   /deep/X.509

.. toctree::
   :maxdepth: 2
   :caption: Reference
   :glob:
   :hidden:

   /reference/*

.. toctree::
   :maxdepth: 2
   :caption: Changelog
   :hidden:

   /release/2.11.x
   /release/2.10.x
   /release/2.9.x
   /release/2.8.x
   /release/2.7.x
