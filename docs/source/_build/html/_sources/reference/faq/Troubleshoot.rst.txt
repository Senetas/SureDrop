.. _Troubleshoot:

Troubleshoot interactions with SureDrop
=======================================

When using or integrating with SureDrop, it may be necessary to work with Senetas engineers
to diagnose problems. Following the steps below will help both you and Senetas diagnose
problems more quickly.

Before reporting issues
-----------------------

..  sidebar:: Note

   SureDrop no longer supports Internet Explorer. Please consider using `Safari <https://support.apple.com/downloads/safari>`_, 
   `Chrome <https://www.google.com/chrome/>`_, `Firefox <https://www.mozilla.org/en-US/firefox/>`_, 
   `Edge <https://www.microsoft.com/en-us/edge>`_, or `Opera <https://www.opera.com/>`_.

Before reporting any issues to Senetas, ensure that you have done the following:

#. Check the :ref:`known-issues` to see if what you're encountering is already known. When
   possible, workarounds will be provided in the issues notes.

#. For on-prem installations, please refer to the :ref:`diag` instructions.   

Fiddler Traces
--------------

The most useful tool when troubleshooting SureDrop issues is `Fiddler <https://www.telerik.com/fiddler>`_. 
When you run Fiddler while reproducing an issue, it will record all HTTP requests and responses. You can then save the Fiddler 
trace and share it with Senetas engineers. Fiddler traces are an invaluable tool when troubleshooting problems because they
provide a full record of the HTTP traffic between the browser and SureDrop. 

Enabling HTTPS decryption in Fiddler
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Because SureDrop traffic is encrypted, Fiddler must be configured to decrypt the HTTPS traffic in order to be
useful. In order to enable HTTPS encryption in Fiddler, do the following:

#. From Fiddler, click :menuselection:`Tools --> Options...` to open the options dialog.
#. On the :guilabel:`HTTPS` tab, check the :guilabel:`Capture HTTPS CONNECTs` check box.
#. Check the :guilabel:`Decrypt HTTPS traffic` check box. When you do this Fiddler will display a dialog asking if you
   wish to trust the Fiddler Root certificate. Click :guilabel:`Yes`. You may also see some security warnings from the
   operating system asking if you want to install the certificate. Click :guilabel:`Yes` to all of these prompts.
#. In the drop-down, select :guilabel:`...from browsers only`.
#. Click :guilabel:`OK` in the options dialog.
#. Close Fiddler and restart it.

Fiddler is now configured to decrypt HTTPS traffic.

..  figure:: ../../images/2.11/fiddler_https.png
    :alt: An image showing the HTTPS decryption configuration UI in Fiddler.

    Fiddler must be configured to decrypt HTTPS traffic in order to produce useful traces

Using Fiddler to trace a session
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Using Fiddler to trace HTTP activity is straightforward:

#. Open Fiddler.
#. If needed, begin capturing traffic (:menuselection:`File --> Capture Traffic`). Note that Fiddler starts in
   capture mode when it is opened, so this step may not be necessary.
#. Navigate to the host page URL while Fiddler is running, then reproduce the issue if needed.
#. Once the issue is reproduced, save the Fiddler session as an archive
   (:menuselection:`File --> Save --> All sessions...`). The resulting file should have the file extension ``.saz``.


Using Fiddler in Linux or OS X
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Fiddler works very well in Windows, but can also be used in Linux and OS X using Mono. See
http://fiddler.wikidot.com/mono for more information on installing and configuring it.

..  _har:

Alternatives to Fiddler: HTTP Archives (HAR)
--------------------------------------------

If you cannot use Fiddler to get session traces, you can also use the Chrome browser developer tools to save HTTP
Archive (HAR) files containing the HTTP requests made by the browser. To do this, do the following:

#.  Open the Chrome developer tools and select the :guilabel:`Network` tab.
#.  Check the :guilabel:`Preserve log` check box if you wish to retain the request log across multiple page
    navigations. This makes the network tracing behave more like Fiddler, and makes it less likely that you'll lose
    your request log by accidentally refreshing the page or navigating away before you save the log. 

    ..  figure:: ../../images/2.11/chrome_network_tab.png
        :alt: An image showing the :guilabel:`Network` tab in the Chrome developer tools.

        :guilabel:`Network` tab in the Chrome developer tools

#.  After you are done reproducing the issue, right-click in the network view and select the
    :guilabel:`Save as HAR with Content` option.

    ..  figure:: ../../images/2.11/chrome_save_as_har.png
        :alt: An image showing the :guilabel:`Save as HAR with Content` option in the Chrome developer tools.

        :guilabel:`Save as HAR with Content` option in the Chrome developer tools

#.  Zip the resulting HAR file, since they can be quite large and generally compress well.

..  tip::
    Other browsers' developer tools have similar capabilities to Chrome to save session HTTP requests as an HTTP
    Archive.
