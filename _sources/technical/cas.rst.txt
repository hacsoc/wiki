CAS
===

Case has deployed JA-SIG's `Central Authentication
Service <https://jasig.github.io/cas/4.1.x/index.html>`_, or CAS,
to allow services to easily authenticate users. The service entered
production use on September 6, 2005.

**Please Note:** This article has been created from an archived copy of the CAS
article from wiki.case.edu.  Although it has been lightly edited, many of the
links are dead, and some of the information is outdated. Efforts have been made
to keep as much information intact as possible, but some sections have been 
removed and some links have been updated.

.. contents:: Table of Contents

Using CAS
---------

Users can log into CAS at https://login.case.edu/cas/. Users can log out of CAS
at https://login.case.edu/cas/logout. If a user logs into CAS, he or she can be
logged in to any application that participates in the service without again
specifying his or her password for a period of up to 8 hours.  Most users do not
visit login.case.edu directly, but instead they are typically redirected there
by client applications.  This process is described below.

Frequently Asked Questions
--------------------------

Why do I need to change my password before I can log in?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CAS integrates with the university's password policy requirements. If your
password is expired and you attempt to log in, CAS will inform you of such. You
will be given a link to change your password.

Why should I close my browser when I am done?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When you log in to CAS, a cookie is stored in your browser that allows you to be
automatically logged in to other sites. This cookie is set to expire at the end
of your browser's session. So, when you close your browser, this cookie no
longer exists and you can no longer be automatically be logged in to any more
sites without specifying your password again.

It is possible to log out of CAS by visiting https://login.case.edu/cas/logout,
however, this is not a secure form of logging out! Some sites may still have you
recorded as logged in through the use of cookies on those specific
sites. Closing your browser is the easiest way to guarantee that the next user
of a computer will not be surfing the web under your identity.

Authentication versus authorization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When you access content, there are two phases you must go through to be allowed
to access it: authentication and authorization. Authentication is proving that
you are who you say you are. Authorization is determining whether a proven
person is *authoriz*\ ed to access something. CAS handles authentication. By
logging in to CAS, CAS can authenticate your identity to participating services
because you have authenticated yourself to CAS and CAS is trusted by the
services that use it. CAS does not handle authorization to individual
services. It is up to the individual services to determine if a user is allowed
to access them.

How do I obtain the user's name, status, etc?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CAS merely authenticates a user. All the services know is that a username,
*abc123* is accessing their site. CAS does not provide information about users
to accessed services. However, all is not lost.  This information is contained
within the university's LDAP server. It is possible for end-services to query
the LDAP server for information about these users to control and customize
service behavior.  Some examples are displaying the user's name, filtering
content based upon user's role within the university (student, staff, faculty,
etc), grade level of student (freshmen, sophomore, junior, senior, etc).

Why should I change my existing service to use CAS?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The simple answer: supplying your password to log in all the time is
annoying. Wouldn't it be convenient to just type your password once every eight
hours and be done with it? Besides, the fewer times users need the password, the
more incentive there is for them to chose a better, more difficult to break,
takes longer to type password.

Contact
~~~~~~~

It appears that the email address sso-admin@case.edu may be able to help, but
this info comes from an old Case Wiki page that may be outdated.

Web Sites and Applications Using CAS
------------------------------------

If you maintain a website that uses CAS, please add your site to the list
below. The sites are listen in chronological order (at least for now).

Deployed
~~~~~~~~

- Case Wiki - wiki.case.edu (since September 6, 2005) (no longer available)
- `Blogs@Case <http://blog.case.edu>`__ (since September 6, 2005)
- `ITS Services <http://its-services.case.edu>`__ (since September 6, 2005)
- Shibboleth (since September 6, 2005)
- `USG Funding System <http://usg.case.edu/funding/>`__ (since September 8, 2005)
- `Bookswap Account Status <http://bookswap.case.edu/acct/>`__ (since September 9, 2005)
- `Software Center <https://softwarecenter.case.edu>`__ (Since September 29, 2005)
- `Lists@Case <http://lists.case.edu>`__ (since October of 2005)
- `Case Screensaver Web Interface <http://photos.case.edu>`__ (since October of 2005)
- Schedule.case.edu (since November 18, 2005) (not a thing anymore)
- `Student Affairs <http://studentaffairs.case.edu>`__ and all related sites (since February 16, 2006)
- `Blackboard <http://blackboard.case.edu>`__ (since February 16, 2006)

Probably a lot more by now.  Really, pretty much every web application at CWRU
is integrated with CAS.

How CAS Works
-------------

Basic overview
~~~~~~~~~~~~~~

When a user accesses a site that uses CAS, that site redirects the user to CAS
(login.case.edu). Once CAS has verified a user's identity, it forwards them back
to the original site. CAS attaches a unique ticket number to the URL of the
protected service. The protected service sees this ticket. It sends this ticket
to CAS. CAS tells the protected service whether the ticket is good and if so,
the Case ID that was used to obtain the ticket. The protected service reacts
accordingly, allowing access if the ticket is good.

Detailed overview
~~~~~~~~~~~~~~~~~

When you log into CAS at https://login.case.edu/cas/, a cookie is saved in your
browser. This cookie contains a unique ticket number that identifies you to the
CAS server. Every time you access https://login.case.edu after you are logged
in, your browser automatically transmits this cookie to the web server. CAS
reads the cookie, looks up the ticket in its database, and identifies you.

CAS clients behave a little differently. Say you access
http://blog.case.edu/mt/mt-cas.cgi. When you load up that page, the page
requires that you be logged into CAS to access it. How does this work?  The page
redirects you to

``https://login.case.edu/cas/login?service=http://blog.case.edu/mt/mt-cas.cgi``

via an HTTP Location header. Once CAS has verified you are logged in, it sends
you back to the URL specified in the *service* parameter, in this case
http://blog.case.edu/mt/mt-cas.cgi. There is, however, one small change. CAS
appends a service ticket to the URL, like

```http://blog.case.edu/mt/mt-cas.cgi?ticket=ST-3555-McPZ4NKfx6S0EhnCEkHc``

The CAS client sees that the *ticket* parameter is defined and knows the
user has just come from https://login.case.edu. The CAS client then
queries

``https://login.case.edu/cas/serviceValidate?ticket=ST-3555-McPZ4NKfx6S0EhnCEkHc&service=http://blog.case.edu/mt/mt-cas.cgi``

The CAS server replies with an XML document that describes the service
ticket. Some of the values returned include whether the ticket is good
and the username associated with the ticket. Alternatively, the CAS
client can query

``https://login.case.edu/cas/validate?ticket=ST-3555-McPZ4NKfx6S0EhnCEkHc&service=http://blog.case.edu/mt/mt-cas.cgi``

This will return a two line document. The first line will say *yes* or
*no*. The next line (only present if the first line is *yes*) will be
the username associated with the ticket.

In short, when a user requests access to an application that is
CASified, that user gets whisked away to the CAS server. Once they are
logged in, the client is returned to the application with a unique
service ticket. This is a personalized ticket, good for only one use,
and a short period of time that will gain you access into the
application. The CAS client verifies this ticket by talking to the CAS
server and if everything checks out, it lets you in.

CAS Implementation Best Practices
---------------------------------

Use Caching
~~~~~~~~~~~

Many of the clients listed below use some form of caching. Without
caching, the CAS client will redirect the user to the CAS server for
every request to obtain a new service ticket. This places more load on
not only the CAS server, but your web server as well. Also, it takes a
little longer for every page access to load because the user has to
process 3 HTTP requests and your web server has to verify the ticket
with the CAS server. Assuming a negligible page load time under normal
conditions, it takes about 5x longer to view a page.

To eliminate this bottleneck, you should store a cookie on the client's
browser that tells your server that they are logged in. This cookie
should contain a ticket that you can map to a user. Most CAS clients do
this transparently. Some clients, such as the PHP client, store this
information in the user's $\_SESSION.

Don't Log the User out of CAS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some CAS clients have a logoff function that will actually log the user
out of CAS. This should be avoided! Don't confuse local application
logoff and CAS logoff. If the user logs out of the local application,
they are simply transitioning from registered user mode to anonymous
user mode. If a user logs out of CAS, they will be forced to supply
their username and password again. A simple way to check for logging out
of CAS is to look for a request to https://login.case.edu/cas/logout. If
this URL is accessed by a client, they will be logged out of CAS.

Configuring Applications to Use CAS
-----------------------------------

CAS is being used because it supports many clients for authentication. A
fairly complete list of clients is
`available <https://jasig.github.io/cas/4.1.x/integration/CAS-Clients.html>`__.
To use CAS for authentication, you need to know the following
parameters:

-  **Host**: https://login.case.edu
-  **Context**: /cas/
-  **Login URL**: https://login.case.edu/cas/login
-  **Logout URL**: https://login.case.edu/cas/logout
-  **Validate URL**: https://login.case.edu/cas/validate (CAS protocol
   version 1)
-  **Service Validate URL**: https://login.case.edu/cas/serviceValidate
   (CAS protocol version 2)
-  **Running Version**: 2.0
-  **CAS Protocol Versions Supported**: 1 and 2

If one the following clients does not work or does not apply to you, you
may wish to create your own CAS client. This is relatively simple
because CAS operates over HTTP and the protocol is relatively simple.
Consulting the `CAS
protocol <https://jasig.github.io/cas/4.1.x/protocol/CAS-Protocol.html>`__
is a necessary step to properly design a client.

Some clients, such as the Apache modules, require that the certificate used by
the login server to be verified. For these, you need to obtain the public
certificate for the Certificate Authority for https://login.case.edu. The
certificate authority is Entrust Server CA and its public certificate can be
found below under the Apache 2 instructions.

Using Apache
~~~~~~~~~~~~

A module, mod\_cas, is available for Apache 1 and 2 to do CAS
authentication. A Perl auth module is also available as an alternative.

Apache 1
^^^^^^^^

Apache 2
^^^^^^^^

Although the version of mod\_cas distributed as part of the CAS client
package is usable, we recommend the use of our custom mod\_cas module.
The advantages of our module are that configuration options for the
module are not compiled into the module. Also, we have modified the
module to work with our modified mod\_auth\_ldap, which can return
dynamic groups from LDAP.

The source code for our module can be found at
https://its-services.case.edu/middleware/src/mod_cas_Apache2.tar.gz. The
development for this module occurs at
http://opensource.case.edu/projects/CAS/.

Extract the contents of this archive anywhere in your filesystem. cd to
the **apache2** directory. Edit the following values in **Makefile**:

-  top\_srcdir
-  top\_builddir
-  srcdir
-  builddir
-  VPATH

The values for *top\_srcdir* and *top\_builddir* are the path to Apache
2's source tree will most likely be identical. An example value would be
*/usr/local/src/httpd-2.0.54*

The values for *srcdir*, *builddir*, and *VPATH* will most likely all be
**./**

The module is compiled and installed by running

.. code:: bash

    make mod_cas.la
    make install-modules

Alternatively, you can compile the module using
`apxs <http://httpd.apache.org/docs/2.0/programs/apxs.html>`__. Run the
following to compile and copy the module to your Apache module
directory:

.. code:: bash

    /path/to/apxs -i -c mod_cas.c ssl_client.c

Once the module is installed, you need to edit your Apache config file
(usually *httpd.conf*) and add the following:

.. code:: apache

    LoadModule cas_module usr/lib/apache2/mod_cas.so
    CASLoginURL https://login.case.edu/cas/login
    CASHost login.case.edu
    CASValidate /cas/validate
    CASTrustedCerts /path/to/entrust.crt
    #CASDebug On

    CASLocalCacheFile /path/to/cas/cache
    CASLocalCacheSize 1000
    CASLocalCacheTimeout 7200
    CASLocalCacheInsecure Off

The **CasTrustedCerts** directive should point to a file containing the public
certificate of the Certificate Authority for the CAS server. It is recommended
to create a file with the following contents:

::

    -----BEGIN CERTIFICATE-----
    MIIE2DCCBEGgAwIBAgIEN0rSQzANBgkqhkiG9w0BAQUFADCBwzELMAkGA1UEBhMC
    VVMxFDASBgNVBAoTC0VudHJ1c3QubmV0MTswOQYDVQQLEzJ3d3cuZW50cnVzdC5u
    ZXQvQ1BTIGluY29ycC4gYnkgcmVmLiAobGltaXRzIGxpYWIuKTElMCMGA1UECxMc
    KGMpIDE5OTkgRW50cnVzdC5uZXQgTGltaXRlZDE6MDgGA1UEAxMxRW50cnVzdC5u
    ZXQgU2VjdXJlIFNlcnZlciBDZXJ0aWZpY2F0aW9uIEF1dGhvcml0eTAeFw05OTA1
    MjUxNjA5NDBaFw0xOTA1MjUxNjM5NDBaMIHDMQswCQYDVQQGEwJVUzEUMBIGA1UE
    ChMLRW50cnVzdC5uZXQxOzA5BgNVBAsTMnd3dy5lbnRydXN0Lm5ldC9DUFMgaW5j
    b3JwLiBieSByZWYuIChsaW1pdHMgbGlhYi4pMSUwIwYDVQQLExwoYykgMTk5OSBF
    bnRydXN0Lm5ldCBMaW1pdGVkMTowOAYDVQQDEzFFbnRydXN0Lm5ldCBTZWN1cmUg
    U2VydmVyIENlcnRpZmljYXRpb24gQXV0aG9yaXR5MIGdMA0GCSqGSIb3DQEBAQUA
    A4GLADCBhwKBgQDNKIM0VBuJ8w+vN5Ex/68xYMmo6LIQaO2f55M28Qpku0f1BBc/
    I0dNxScZgSYMVHINiC3ZH5oSn7yzcdOAGT9HZnuMNSjSuQrfJNqc1lB5gXpa0zf3
    wkrYKZImZNHkmGw6AIr1NJtl+O3jEP/9uElY3KDegjlrgbEWGWG5VLbmQwIBA6OC
    AdcwggHTMBEGCWCGSAGG+EIBAQQEAwIABzCCARkGA1UdHwSCARAwggEMMIHeoIHb
    oIHYpIHVMIHSMQswCQYDVQQGEwJVUzEUMBIGA1UEChMLRW50cnVzdC5uZXQxOzA5
    BgNVBAsTMnd3dy5lbnRydXN0Lm5ldC9DUFMgaW5jb3JwLiBieSByZWYuIChsaW1p
    dHMgbGlhYi4pMSUwIwYDVQQLExwoYykgMTk5OSBFbnRydXN0Lm5ldCBMaW1pdGVk
    MTowOAYDVQQDEzFFbnRydXN0Lm5ldCBTZWN1cmUgU2VydmVyIENlcnRpZmljYXRp
    b24gQXV0aG9yaXR5MQ0wCwYDVQQDEwRDUkwxMCmgJ6AlhiNodHRwOi8vd3d3LmVu
    dHJ1c3QubmV0L0NSTC9uZXQxLmNybDArBgNVHRAEJDAigA8xOTk5MDUyNTE2MDk0
    MFqBDzIwMTkwNTI1MTYwOTQwWjALBgNVHQ8EBAMCAQYwHwYDVR0jBBgwFoAU8Bdi
    E1U9s/8KAGv7UISX8+1i0BowHQYDVR0OBBYEFPAXYhNVPbP/CgBr+1CEl/PtYtAa
    MAwGA1UdEwQFMAMBAf8wGQYJKoZIhvZ9B0EABAwwChsEVjQuMAMCBJAwDQYJKoZI
    hvcNAQEFBQADgYEAkNwwAvpkdMKnCqV8IY00F6j7Rw7/JXyNEwr75Ji174z4xRAN
    95K+8cPV1ZVqBLssziY2ZcgxxufuP+NXdYR6Ee9GTxj005i7qIcyunL2POI9n9cd
    2cNgQ4xYDiKWL2KjLB+6rQXvqzJ4h6BUcxm1XAX5Uj5tLUUL9wqT6u0G+bI=
    -----END CERTIFICATE-----

and set this directive to point to that file.

You can use the *CASDebug* directive to allow extra debugging to the
Apache log for testing purposes. For *CASLocalCacheFile*, create a blank
file and set its permissions so the Apache user can write to this file.

To protect a specific directory to require CAS authentication, just use
AuthType CAS. For example:

.. code:: apache

    <Location "/cas-protected/">
        AuthType CAS
        AuthName "CAS"
        require valid-user
    </Location>

By default, the CAS module will handle authentication and authorization.
If you have another module that you would like to process authorization,
such as mod\_auth\_ldap, you need to tell mod\_cas to defer to that
module. This is done by adding the directive **CASAuthenticateOnly On**
to either the global httpd.conf file or in any , , , or .htaccess
location. You can set **CASDebug On** and view the Apache error log to
verify everything is working as it should.

Apache 2.2
^^^^^^^^^^

The Apache 2.0 module is not compatible with Apache 2.2 due to Apache API
changes. Gregory Szorc will be working on writing a CAS module for Apache
2.2. If you have an urgent need for this module, let him know.

IIS
~~~

- `CAS ISAPI filter for ISS <http://jasigch.princeton.edu:9000/display/CAS/ISAPI+Filter>`__
  (*dead link, sorry*)
- `CCCI CAS <http://gcx1.mygcx.org/cas/CCCIChanges.html>`__
  alternative plugin for ISS/Apache (see
  `documentation <http://gcx1.mygcx.org/cas/web-server-agent/doc/CasAgentDoc.html>`__)
  (*also dead links*)

*These filters are not well supported, and may not even work at all. If
you are successful in implementing any ISAPI filters, please add
instructions for doing so here.*

PHP
~~~

There are two PHP libraries that can be used with CAS at Case. The Case CAS
Module is very simple. It requires PHP 5 to run.  phpCAS supports all the bells
and whistles of CAS, but requires a little more setup.

Case CAS Module
^^^^^^^^^^^^^^^

Information about this module is available at
http://opensource.case.edu/projects/CaseClasses/. The source code is
available at
http://opensource.case.edu/svn/CaseClasses/php/trunk/Case/Authn/CAS.php.

**Note:** Both links above are dead.  Updated sources for the Case CAS module
(if it still exists) would be very much appreciated.

Sample usage:

.. code:: php

    require_once('Case/Authn/CAS.php');
    $cas = new Case_Authn_CAS();
    $cas->forceAuthentication();
    $CaseID = $cas->getCaseID();

or

.. code:: php

    require_once('Case/Authn/CAS.php');
    $cas = new Case_Authn_CAS();
    $cas->checkAuthentication();

    if ($cas->isLoggedIn()) {
      //the user is known to be logged in
      //do whatever you want with them
    }

phpCAS
^^^^^^

You can use `phpCAS <http://esup-phpcas.sourceforge.net/>`__, a CAS PHP
library to perform CAS authentication within your PHP applications.

To install phpCAS, download phpCAS, extract the contents of the archive,
and copy *source/CAS* to somewhere in PHP's *include\_path*. In your PHP
application, use the following to set up your CAS client:

.. code:: php

    require_once('CAS/CAS.php');

    phpCAS::client(CAS_VERSION_2_0,'login.case.edu',443,'/cas');

The creation of the phpCAS client automatically calls session\_start
unless the 5th parameter of the function is *false*. If your session is
already started, this will issue a PHP warning.

To force the user to be logged in, execute the following statement:

.. code:: php

    phpCAS::forceAuthentication();

If you need to obtain the person's network ID, use:

.. code:: php

    $NetID = phpCAS::getUser();

More documentation is availabe at the library's web site.

**Do not use *phpCAS::logout()* in your script, as it will log the user
out of CAS**. Instead, you can perform a local logout by manipulating
$\_SESSION variables or cookies.

Example PHP Script
^^^^^^^^^^^^^^^^^^

.. code:: php

    <?php

    //initialize the CAS library
    require_once('CAS/CAS.php');
    phpCAS::client(CAS_VERSION_2_0, 'login.case.edu', 443, '/cas');

    //if the user is requesting to be logged in
    if (isset($_REQUEST['login'])) {
       phpCAS::forceAuthentication();
       //the user is known to be logged in to CAS at this point
       $_SESSION['loggedInLocally'] = true;  //set a local variable telling the program we are logged in
       $_SESSION['username'] = phpCAS::getUser();  //this stores their network user id
    }

    //if we want to log out of the program
    if (isset($_REQUEST['logout'])) {
       $_SESSION['loggedInLocally'] = false;
       unset($_SESSION['username']);
    }

    if (isset($_SESSION['loggedinLocally']) && $_SESSION['loggedInLocally']===true) {
       echo "You are logged in to the application";
    } else {
       echo "You are not logged in to the application.  Log in by specifying the 'login' log parameter to this script.";
    }

    ?>

Perl
~~~~

(Old: See http://sourcesup.cru.fr/perlcas/. )
This link is dead! If you use CAS with Perl and find an appropriate resource,
please update this wiki with it! (A Web search for PerlCAS might yield a good
resource(s).)

Java
~~~~

(Old: See http://jasigch.princeton.edu:9000/display/CAS/Java+Client. )
This link is dead! If you use CAS with Java and find an appropriate resource,
please update this wiki with it!

Ruby / Ruby on Rails
~~~~~~~~~~~~~~~~~~~~

`RubyCAS <https://github.com/rubycas>`_ has a client and server implementation.
For integrating with Case CAS, just look at the client implementation.

Django
~~~~~~

Most modules for CAS in Django are named "django-cas" or something similar, so
they're rather difficult to tell apart.  Here are a couple distinct ones, you'll
have to try a couple out and see which ones work for you.

- `django-cas <https://github.com/castlabs/django-cas>`_
- `django-cas2 <https://github.com/KTHse/django-cas2>`_
