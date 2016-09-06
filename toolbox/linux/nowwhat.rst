I Installed It!  Now What?
==========================

Congratulations! If everything worked properly, you should be looking at a
freshly installed Linux login screen, either inside a virtual machine or "for
real for real" on your main computer.

What to do from here is up to you. The Toolbox pages after this one give some
great things to learn to do on Linux. However, here are some other things you
may want to do besides the technical stuff.

*Note that the commands in code blocks below should be run in your Terminal
program on Linux.  Also, these assume you installed Ubuntu.*

How Do I Install Stuff?
-----------------------

Every Linux distribution has its own package manager, and so the instructions
may be slightly different depending on your distro. If you did Ubuntu, all you
need to do is run:

.. code::

   sudo apt install <package name>

Typically the package name is exactly what you'd expect, but lower case. For
example, ``git``, ``python``, ``firefox``, etc. However, sometimes it may have a
slighly different name from expected. You can search for packages `online
<http://packages.ubuntu.com>`_.

Sometimes, software that you want may not be packaged, but their site may offer
Linux downloads in ``.deb`` or ``.rpm`` format. In these cases, you can download
the ``.deb`` (not the RPM!) and double click that to install it.

Is There An Easier Way to Install Stuff?
----------------------------------------

Yeah, there's something called the Ubuntu Software Center (you should be able to
find it in the menu). You can use that to search and install programs, similar
to the Mac/Windows app stores. However we'd recommend that you get used to a
command-line package manager.

Where's Google Chrome?
----------------------

One common one that may trip you up is Chrome. In the Linux world, there are two
versions of Chrome: *Google Chrome* and *Chromium*. *Chromium* is an open source
web browser project that *Google Chrome* is based on. As such, it is almost
always in your package manager as ``chromium``. Google Chrome is simply Chromium
plus a built-in PDF reader, a Flash plugin, and a Google-colored icon. It's
easiest to install Chromium by simply doing:

.. code::

   sudo apt install chromium

However, if you really want that PDF reader and Flash plugin, you can install
Google Chrome by downloading the ``.deb`` file from Google's Chrome page, double
clicking that, and installing it through the Ubuntu Software Center.

What's a PPA?
-------------

PPA's are sources of third-party software. Basically, although plenty of stuff
is in Ubuntu's package archives, not everything is. Sometimes, the stuff in
Ubuntu's archives is a bit old. PPA's can solve both problems.

Typically, when you're Googling how to install a program, they'll give you a PPA
name and a package name. The PPA name has a slash in it. The typical steps for
using a PPA are:

.. code::

   sudo add-apt-repository ppa:<PPA NAME HERE>
   sudo apt update
   sudo apt install <PACKAGE NAME>

For instance, to install Sublime Text 3 (an editor that's probably discussed in
the Editors section of the Hacker's Toolbox):

.. code::

   sudo add-apt-repository ppa:webupd8team/sublime-text-3
   sudo apt update
   sudo apt install sublime-text-installer

It's important to keep in mind that adding a source of software to your system
has the potential to do damage if you don't trust the source. The example above
is WebUpd8Team, a fairly well known source of PPA's. In general, try to do a
little research before you simply add a PPA.

What Do I Use Instead of Microsoft Office?
------------------------------------------

Google Drive is an excellent alternative (especially since you have tons of
storage through CWRU).  It works in Firefox, Chromium, or Google Chrome.

If you still want an office suite (say for opening and editing documents
locally), try LibreOffice. It typically comes preinstalled on Ubuntu, and it has
equivalents for Word, Excel, and Powerpoint (as well as a few others). It's
quite good and reasonably compatible with MS Office, but it's not perfect.

If you're looking for a nice way to do your homework on Linux (and you're
interested in learning a new language/tool), check out LaTeX. It's a steep
learning curve, but it produces good-looking documents. It's also the standard
for academic conference/journal articles in the Math and CS world, so it's a
quite good tool to learn. Google it for more info!

What Do I Use Instead of Photoshop?
-----------------------------------

Try GIMP (aka GNU Image Manipulation Program).

What Do I Use Instead of X?
---------------------------

These are great things to Google! If you're really having trouble, you can ask
around in Slack or the mailing list for recommendations.

Other Stuff
-----------

There are plenty of suggestions for improving your life after installing Ubuntu.
These include making Ubuntu look prettier or behave more to your liking. A
Google search like "what to do after installing ubuntu" could bring up useful
results like `this one
<http://www.omgubuntu.co.uk/2016/04/10-things-to-do-after-installing-ubuntu-16-04-lts>`_.
