OK I'm Ready... How Do I Try/Install It?
========================================

So you're ready to install a Linux? Great! If it's your first time, hopefully
you're starting with Ubuntu. Also if it's your first time, you may want to grab
an experienced Linux buddy (ask in Slack or mailing list) to help you. Don't do
this if you know you'll desperately need your computer the next day!

*If you're not installing Ubuntu, these steps may not apply perfectly to you.*
The information on virtual machines, live CDs, and live USBs will probably be
helpful though.

Step 1: Download
----------------

If you haven't already, download your Linux. It should be a file ending in
``.iso``, and if there are many options, you'll probably want the amd64 one
(unless you know you have a 32-bit computer). It will likely be several hundred
megabytes in size, and so the download might take a while.

Step 2: Try it in a Virtual Machine
-----------------------------------

Installing Linux **replaces** your existing operating system, **overwriting**
all of your programs and files on your computer. If you're not ready to
completely jump ship to Linux, this is a bit impractical. Ideally, you should
try it out before committing to using it full time. You can do this with a
virtual machine!

Virtual machines are exactly what they sound like: programs that pretend to be
an entire computer. They let you install entire operating systems inside of them
without modifying anything on your computer. We recommend using `VirtualBox
<https://www.virtualbox.org/>`_.

Once you've installed VirtualBox, run it and click "New". This will guide you
through the creation of a virtual machine. Make sure to name it after the Linux
distro you're installing (e.g. Ubuntu), which should automatically select the
right machine type. The default settings in this wizard are all fine, but if you
have a computer with lots of memory you may benefit from using 2048 MB of RAM
instead of 1024.

Once you've created the VM, you'll need to "insert" your distribution's ISO file
into it. You can do this by going to "Settings" and clicking the "Storage" tab
along the side. Select "Controller: IDE" and click the icon that shows a CD with
a plus sign. When it prompts, select "Choose Disk" and select your ISO file. Hit
OK to save your settings.

Now, in the main VirtualBox window, you can hit "Start" to turn on your virtual
computer. It will boot from your ISO file and (if you use Ubuntu) present you
with an installer that will walk you through setup. Pretty much everything can
be left at its defaults.

Once the installation completes (this may take a while), you can go into
VirtualBox's settings, remove the ISO disk, and reboot the VM. Voila! Linux is
installed on your VM!

Now try things out! Mess around with the terminal, maybe try out some other
parts of the "Hacker's Toolbox" section. If you decide you like it (and you
don't mind wiping your computer), you can continue these steps to install it to
your computer. If you don't like the distro you chose, just delete the VM and
try a new one!

Step 3: Live USB
----------------

The next step to installing Linux is putting it on a CD or USB flash drive.
Since part of the installation procedure is wiping your hard drive, you can't
just install straight from the ISO file. So, you install Linux by putting the
contents of the ISO file on a CD or USB, and then rebooting your computer to run
the installer.

The easiest is to use a USB, since they are rewritable and every computer has a
USB drive. You'll need an empty USB drive (or one whose contents you don't care
about) to do this.

Ubuntu has excellent instructions on doing this:

- `For Windows
  <http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-windows>`_
- `For Mac OS X
  <http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-mac-osx>`_

Step 4: Install to Your Computer
--------------------------------

At this point, you should be confident that you want to replace your existing
operating system and erase all of your files (back up **EVERYTHING** important).
If this is your main computer, you ought to be confident that you can do
everything (homework, entertainment, etc) on your chosen distribution. Try the
VM approach above if you're not sure.

The steps for this are deceptively simple:

1. Plug in the USB stick.
2. Reboot your computer. Hopefully it will boot from the USB stick. If not, try
   rebooting and holding down one of the following keys: F8 through F12, or
   Escape. Usually one of these will bring up a menu where you can select what
   you want to boot from. Select your USB stick from this device.
3. Follow the install menu (hopefully you already did this when you tried it in
   a VM!).  You'll probably need to remove the USB drive when you reboot.

If you see an option in your installer to "try without installing" or "boot live
USB", this usually means that it will start up a full version of the Linux
you're about to install, but *without actually installing it*. This is another
great way to try out a Linux distribution! It's especially nice because it uses
your computer's actual hardware - if it doesn't work Live, you may have a
problem installing it.
