WMI - Windows Management Instrumentation
========================================

What is it?
-----------

Windows Management Instrumentation (WMI) is Microsoft's implementation of
Web-Based Enterprise Management (WBEM), an industry initiative to provide
a Common Information Model (CIM) for pretty much any information about a
computer system.

The Python WMI module is a lightweight wrapper on top of the pywin32
extensions, and hides some of the messy plumbing needed to get Python to
talk to the WMI API. It's pure Python and has been tested against all
versions of Python from 2.5 to 3.4. It should work with any recent
version of pywin32.


Where do I get it?
------------------

* **PyPI**: https://pypi.python.org/pypi/WMI/
* **Github**: https://github.com/tjguk/wmi


How do I install it?
--------------------

::

    pip install wmi


How do I use it?
----------------

Have a look at the :doc:`tutorial` or the :doc:`cookbook`. As a quick
taster, try this, to find all Automatic services which are not running
and offer the option to restart each one::

    import wmi

    c = wmi.WMI()
    for s in c.Win32_Service(StartMode="Auto", State="Stopped"):
        if raw_input("Restart %s? " % s.Caption).upper() == "Y":
            s.StartService()

What's Changed?
---------------

See the :doc:`changes` document

Copyright & License?
--------------------

* Copyright Tim Golden <mail@timgolden.me.uk> 2003 - 2015

* Licensed under the (GPL-compatible) MIT License:
  http://www.opensource.org/licenses/mit-license.php

Prerequisites
-------------

If you're running a recent Python (2.5+) on a recent Windows (2k, 2k3, 2012, XP, Vista, 7, 8.x)
and you have Mark Hammond's win32 extensions installed, you're probably
up-and-running already. Otherwise...


Python
~~~~~~
http://www.python.org/

pywin32 (was win32all)
~~~~~~~~~~~~~~~~~~~~~~
http://sourceforge.net/projects/pywin32/files/

Specifically, builds 154/155 fixed a problem which affected the WMI
moniker construction. You can still work without this fix, but some
more complex monikers will fail. (The current build is 219 so you're
probably ok unless you have some very stringent backwards-compatible
requirement).

makepy
~~~~~~
(NB my own experience over several systems is that this
step isn't necessary. However, if you have problems...)
You may have to compile makepy support for some typelibs. The following
are reported to be significant:

* Microsoft WMI Scripting Library
* WMI ADSI Extension Type Library
* WMICntl Type Library

If you've not done this before, start the PythonWin environment, select
Tools > Com Makepy utility from the menu, select the library by name, and
click [OK].
