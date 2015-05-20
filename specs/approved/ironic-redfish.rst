..
 This work is licensed under a Creative Commons Attribution 3.0 Unported
 License.

 http://creativecommons.org/licenses/by/3.0/legalcode

=========================
Redfish driver interfaces
=========================

https://bugs.launchpad.net/ironic/+bug/1526477

This specification proposes the addition of a new driver in order to support
Ironic deployment on Redfish compliant servers.

Problem description
===================

The Distributed Management Task Force (DMTF) has published a new specification
called Redfish (refer to http://www.dmtf.org/standards/redfish) to provide a
RESTful based API to manage servers in a standard way. This specification aims
at adding support to Ironic for controlling Redfish compliant servers.

Proposed change
===============

Power and management interfaces will be extended with Redfish support.
The new Redfish module uses the python-redfish library for communicating with
a Redfish system.
(refer to https://git.openstack.org/cgit/openstack/python-redfish)

The goal is to provide power management similarly to what is done
in the pre-existing in-tree drivers.

Note that no OEM specific extension will be supported.

Alternatives
------------
No real alternative exists currently

Data model impact
-----------------
None

RPC API impact
--------------
None

State Machine Impact
--------------------
None

REST API impact
---------------
None

Driver API impact
-----------------
None

Nova driver impact
------------------
None

Ramdisk impact
--------------
None

Security impact
---------------
None

Client (CLI) impact
-------------------
None

Other end user impact
---------------------
None

Scalability impact
------------------
None

Performance Impact
------------------
None

Other deployer impact
---------------------
The following driver_info fields are required while enrolling nodes into Ironic:
    * redfish_uri URI of the System to interact with
      (e.g.: http://x.y.z.t/redfish/v1/Systems/1 or
      https://redfishmgr/redfish/v1/Systems/CX34R87)
    * redfish_username: User account with admin/server-profile access privilege
    * redfish_password: User account password

Developer impact
----------------
None

Implementation
==============

Assignee(s)
-----------

Primary assignee:
bcornec

Other contributors:
ribaudr

Work Items
----------

* Add new Redfish hardware type, supporting power and management interface
  APIs and providing PXE, virtual media boot and standard deployment
  methods.
* Writing unit-test cases for the Redfish type.
* Develop Redfish support for the virtualbmc project.
* Adaptation of the devstack Ironic module to add this capability, based
  on the virtualbmc work, adding to it the minimal required Redfish REST
  API support.
* Writing configuration documents.

Dependencies
============
This driver requires python-redfish installed on the conductor node.

Testing
=======
Unit-tests will be implemented for Redfish support.
Continuous integration (CI) support will be added for Redfish servers.

Redfish support will be also developed for the virtualbmc project so the
standard Ironic tests can be performed, but using this protocol.
The DMTF provides a Redfish mockup. It can been launched easily to allow
testing against it.

Upgrades and Backwards Compatibility
====================================
This driver will not break any compatibility with either the REST API or
the RPC API.

Documentation Impact
====================
* Writing configuration documents.
* Updating Ironic documentation section _`Enabling Drivers`:
  http://docs.openstack.org/developer/ironic/deploy/drivers.html with Redfish
  related instructions.
* Updating Ironic install-guide documentation section
  _`Setup the drivers for the Bare Metal service`:
  http://docs.openstack.org/project-install-guide/baremetal/draft/setup-drivers.html

References
==========

_`Redfish DMTF`: http://www.dmtf.org/standards/redfish
_`python-redfish`: https://git.openstack.org/cgit/openstack/python-redfish
