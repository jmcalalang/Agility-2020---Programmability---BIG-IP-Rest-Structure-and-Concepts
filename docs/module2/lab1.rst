Lab 2.1: Exploring AS3
----------------------

Installation
~~~~~~~~~~~~

iControl LX Extensions use the standard Redhat Package Manager (RPM) distribution format.  To install an extension, you need first to obtain the RPM file associated with the extension.

AS3 RPMs are available at https://github.com/f5networks/f5-appsvcs-extension/releases

AS3 can be installed in a few ways:

- using the iControl REST API
- using the BIG-IP GUI (TMUI)
- using a command prompt

All of these mechanisms are supported and, if required, can be used in
conjunction with each other.

For instance, you can install AS3 from BIG-IP GUI and then deploy
a new service via iControl REST using tools such as cURL, Postman
and Ansible.

To view installed iControl LX Extensions in the BIG-IP GUI you must first
enable this functionality.  To do this, log in via SSH into the system with an ``admin`` account and execute ``touch /var/config/rest/iapps/enable``. No reboot is required. This will enable the :menuselection:`iApps > Package Management LX` menu:

|lab-1-1|

Clicking :guilabel:`Package Management LX` will show a table of installed iControl LX Extensions:

.. NOTE:: This will be empty until one or more iControl LX Extension packages have been imported.

|lab-1-2|

Deployments
~~~~~~~~~~~

.. NOTE:: Redeployment of AS3 services is facilitated/protected by a mechanism in the BIG-IP platform to ensure safe changes to the configurations without disrupting existing user traffic.

iControl LX allows Extensions to register new REST API endpoints with the iControl REST API.  In the case of AS3 the following endpoints are exposed:

- **Version Info:** ``/mgmt/shared/appsvcs/info``
- **Declarations:** ``/mgmt/shared/appsvcs/declare``

Deployments use the `/mgmt/shared/appsvcs/declare` endpoint.  This endpoint accepts the Create, Read, Update and Delete (CRUD) operations using the HTTP ``POST``, ``GET``, ``PATCH`` and ``DELETE`` methods.

Additionally, various query parameters are also supported.  Full documentation is available in the `AS3 Reference <http://clouddocs.f5.com/products/extensions/f5-appsvcs-extension/3/refguide/as3-api.html>`_

Source-of-Truth
~~~~~~~~~~~~~~~

In an automated environment, we **must** always ensure that the
**AS3 declarations** are being used as the Source-of-Truth for an underlying deployment.  Therefore, you should **NOT** perform out-of-band modifications to the configuration using the BIG-IP GUI or REST API.

For instance, after an AS3 declaration is deployed, modifying the underlying configuration will result in a Source-of-Truth violation.  AS3 **does not** prevent out-of-band changes from occurring.  This allows administrators to ensure total control over the system in emergency situations. However, the direct modification of objects configured on BIG-IP will affect the integrity of the AS3 declaration that automation tools are interacting with, causing failures. It is, therefore, essential to prevent out-of-band changes at all times for automated deployments in normal production circumstances.

.. |lab-1-1| image:: images/lab-1-1.png
.. |lab-1-2| image:: images/lab-1-2.png
   :scale: 80%
