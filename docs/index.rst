Why Picked this Section
-----------------------

I chose `Installation and Getting Started <https://docs.pytest.org/en/latest/getting-started.html>`_ because I knew nothing about pytest and wanted to learn.

How Improved
------------

When I began installing and testing pytest on my mac, it became clear that several information gaps existed in the doc. I added the following new sections based on the snags I hit during my user experience:

* :ref:`pyinstall` -- I wanted to test using Python 3.5 with the latest pytest package. However, the doc lacked Python installation instructions for my Mac OS X version. 
* :ref:`pip3` -- It was not clear that ``pip3`` was required to install pytest for Python 3.5, so I added a new section about this. I also included a tip on how to use ``source`` to reload a ``.bash_profile``.
* :ref:`swver` -- It was not clear how to verify the software versions that are paired together to run pytests.
* :ref:`cache` -- After I ran my first test, two cache stores were created. These were not documented anywhere in the guide. 
* :ref:`asserts` -- My test was not displaying results until I added assert statements. This step might be obvious to most Python experts but wasn't to me. Anyways, I added a section about it. 
* :ref:`collection` -- I kept getting collection errors during my testing. There was no section about how to troubleshoot this kind of error in the docs. The 200 page PDF didn't help either.
* :ref:`git` -- Depending on the team and project, I like to give developers an opportunity to update the docs directly (no tech writer bottleneck). My new sections are stored in this `Git Ubertest Repo <https://github.com/gmcmillan100/ubertest/tree/master/docs>`_ and can be updated using the standard Git workflow.
* Search -- The existing doc lacked an obvious search box and a clean navigation, so I wrote my new sections inside a Sphinx framework with a custom Uber theme. :-)

.. _pyinstall:

Python 3.5 Installation for Mac 10.11
-------------------------------------

Follow these steps to install a 32-bit i386/PPC version of Python 3.5 on Mac OS X El Capitan:

1. Download the package at `python-3.5.3-macosx10.5.pkg <https://www.python.org/ftp/python/3.5.3/python-3.5.3-macosx10.5.pkg>`_.

2. Open the package installer, accept the license, and install the software.

3. From the terminal, issue ``python3 -V`` to display the installed version::

	$ python3 -V
	Python 3.5.3

4. Use ``which python3`` to display the installation location::

	$ which python3
	/usr/local/bin/python3

.. _pip3:

Pytest 3.1.3 Installation for Python 3.5
----------------------------------------

1. Use ``pip3 install -U pytest`` to download and install pytest and its dependencies::

	$ pip3 install -U pytest
	Collecting pytest
	  Downloading pytest-3.1.3-py2.py3-none-any.whl (181kB)
	    100% |||||||||||| 184kB 2.6MB/s 
	Collecting py>=1.4.33 (from pytest)
	  Downloading py-1.4.34-py2.py3-none-any.whl (84kB)
	    100% |||||||||||| 92kB 7.2MB/s 
	Collecting setuptools (from pytest)
	  Downloading setuptools-36.2.0-py2.py3-none-any.whl (477kB)
	    100% |||||||||||| 481kB 1.6MB/s 
	Installing collected packages: py, setuptools, pytest
	  Found existing installation: setuptools 28.8.0
	    Uninstalling setuptools-28.8.0:
	      Successfully uninstalled setuptools-28.8.0
	Successfully installed py-1.4.34 pytest-3.1.3 setuptools-36.2.0

2. Issue the ``source`` command to reload the ``.bash_profile`` in your home directory and apply the path update to your active shell session::

	$ source ~/.bash_profile

3. Display the installed version of pytest by using ``pytest --version``::

	$ pytest --version
	This is pytest version 3.1.3, imported from /Library/Frameworks/Python.framework/Versions/3.5/lib/python3.5/site-packages/pytest.py

.. _swver:

Software Version Dependencies
-----------------------------

The top output line of ``pytest`` displays the software versions that are used to process the test and in what directory. This information is useful for troubleshooting your downstream package dependencies::

	$ pytest
	============= test session starts ===================
	platform darwin -- Python 3.5.3, pytest-3.1.3, py-1.4.34, pluggy-0.4.0
	rootdir: /Users/McMillan/greg/uber-test, inifile:
	collected 1 item s

	test_sample.py F

	================== FAILURES =======================
	...

.. _cache:

Cache System Files
------------------

After a test runs, two cache stores are created inside the test directory. See ``__pycache__`` and ``.cache``::

	__pycache__/test_sample.cpython-35-PYTEST.pyc
	.cache/v/cache/lastfailed

Use these caches as historical audit logs for your tests.

.. _asserts:

Asserts for Pytests
-------------------

If an ``assert`` statement does not exist in your code, pytest will not display any assertion errors. An assert statement tells the program to test a condition and trigger an error if the condition is false.

For example, this code does not contain an assert::

	def func(x):
	    return x + 1

	def test_answer():
	    func(3) == 5

When pytest runs, no assertion error is reported::

	$ pytest test_sample.py 
	======================== test session starts =============================
	platform darwin -- Python 3.5.3, pytest-3.1.3, py-1.4.34, pluggy-0.4.0
	rootdir: /Users/McMillan/greg/uber-test, inifile:
	collected 1 item s

	test_sample.py .

	======================= 1 passed in 0.02 seconds =====================

When an ``assert`` statement is added::

	def test_answer():
	    assert func(3) == 5

Pytest displays the error::

	$ pytest test_sample.py 
	=================== test session starts ==============================
	platform darwin -- Python 3.5.3, pytest-3.1.3, py-1.4.34, pluggy-0.4.0
	rootdir: /Users/McMillan/greg/uber-test, inifile:
	collected 1 item s

	test_sample.py F

	======================= FAILURES =====================================
	_______________________ test_answer ________________________________________

	    def test_answer():
	>       assert func(3) == 5
	E       assert 4 == 5
	E        +  where 4 = func(3)

	test_sample.py:5: AssertionError
	====================================== 1 failed in 0.06 seconds =====================

.. _collection:

Troubleshooting Collection Errors
---------------------------------

A collection error is different from a failed test. The collection phase is when pytest walks through your files, looking for test modules and test functions. If you get a collection error, check that your modules are defined correctly::

	_________________________ ERROR collecting test_apple.py ______________________
	test_apple.py:42: in <module>
	    assert countDown()
	E   assert None
	E    +  where None = <function countDown at 0x21a2464>()
	------------------------------------------------ Captured stdout --------------------------------
	!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Interrupted: 1 errors during collection !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
	============================================ 1 error in 0.27 seconds ============================================

.. _git:

Adding to this Doc Using Git
----------------------------
This document is stored in this `Uber Test Git repo <https://github.com/gmcmillan100/ubertest/tree/master/docs>`_.

Do the following to copy the repo to your local computer::

$ mkdir ubertest
$ cd ubertest
$ git init .
$ git remote add origin git@github.com:gmcmillan100/ubertest.git
$ git pull git@github.com:gmcmillan100/ubertest.git master

Then, follow the standard Git workflow to update the files::

$ git add index.rst
$ git commit -m "Adding an enhancement"
$ git push


.. toctree::
   :depth: 1



