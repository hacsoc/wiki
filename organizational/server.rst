HacSoc/ACM server
=================

CWRU ACM controls a server, donated by alumni.  This server should be used to
host applications and services that are useful to students.

Usage policy
------------

The Hacker Society :ref:`code-of-conduct` applies to any externally facing
service hosted on the ACM server.  This includes websites and chat services.
It does not include private services, such as private chats or sites that are
protected by a password.

The CWRU `Acceptable Use of Information Technology Policy
<http://www.case.edu/utech/policies/i-1-acceptable-use-of-information-technology-policy-aup/>`_
applies to all services, public or private.

Server admin
------------

The server admin will be apointed by the HacSoc officers, and is responsible
for administrating and maintaining the ACM server and all services on it.  He
or she may recruit assistant server admins to help with this duty.

As the person responsible for administrating and maintaining all services on
the ACM server, the server admin reserves the right to decide which services
will run on the server.

The current server admin is `Matthew Bentley <mailto:bentley@case.edu>`_.

Past server admins
^^^^^^^^^^^^^^^^^^
- Even Krall
- Josh Snyder
- Cameron Gutman
- Aaron Neyer

Services
--------

Krall
^^^^^^^^^^^^^^
Krall (krall.case.edu) is the nickname of the main server.  It is running
Ubuntu 14.04 on bare metal, and hosts the rest of the services listed below.

Krall also runs
~~~~~~~~~~~~~~~
- DNS for acm.case.edu
- Nagios monitoring (currently not maintained)

Virtual Machines
^^^^^^^^^^^^^^^^

Active
~~~~~~
- `IRC <http://irc.case.edu>`_
- `ACM People <http://people.acm.case.edu>`_
- `APO <http://apo.case.edu>`_
- `HKN <http://hkn.case.edu>`_
- `Docker hosting`_

Not Active
~~~~~~~~~~
There are also a bunch of VMs that don't get turned on, including a Minecraft
server and several student project servers.

Docker hosting
^^^^^^^^^^^^^^

The docker hosting server is designed primarily to run websites, but will run
anything that runs in docker and needs a <something>.case.edu hostname and
a network connection.  There is currently limited documentation.  Contact
`Matthew Bentley <mailto:bentley@case.edu>`_ for more info.

Services
~~~~~~~~
- `UMB website <http://mediaboard.case.edu>`_
- `ACM website <http://acm.case.edu>`_
- `Auth server <https://github.com/hacsoc/auth>`_
- `Food Recovery Network website <http://frn.case.edu>`_
- `Swing club website <http://swingclub.case.edu>`_
- `The Jolly Advisor <http://advise.case.edu>`_
- `SlackSoc <https://github.com/hacsoc/slacksoc>`_
- `CWRUbotix website <http://cwrubotix.case.edu>`_
- `OX-Dashboard (Theta Chi internal dashbaord) <http://oxdashboard.case.edu>`_

Possible Future Services
^^^^^^^^^^^^^^^^^^^^^^^^
- Email server
- Monitoring system (eg Nagios or Sensu)
- Game servers
