Why I Picked this Section
-------------------------

https://docs.pytest.org/en/latest/getting-started.html

How you improved this section
A 1-2 paragraph summary of the information in the section, assuming modest technical knowledge of the reader
This submission will measure your aptitude for writing about technical subjects as well as pure writing ability. A submission showcasing proper grammar, spelling, punctuation, and technical writing style and conventions is as important as the content itself.

I wanted to test pytest using Python 3.5 on my mac, I had to install Python 3.5. Hit a few installation snags along the way. Adding them in my version. 

The Python 3 commands are different from Python 2. 

Doc assumes people have Python already installed. I did not. Show how to install. 

Not clear how to identify the software versions used to run against a test.

After I ran my first test, two cache stores where created. These were not documented anywhere in the guide. 

My test was displaying no results until I added an assert statement to my code. 

Python 3.5 Installation for Mac 10.11
-------------------------------------

Follow these steps to install a 32-bit i386/PPC version of Python 3.5 on Mac OS X El Capitan.

1. Download the package at `python-3.5.3-macosx10.5.pkg <https://www.python.org/ftp/python/3.5.3/python-3.5.3-macosx10.5.pkg>`_.

2. Open the package installer, accept the license, and install the software.

3. From the terminal, issue ``python3 -V`` to display the installed version::

	$ python3 -V
	Python 3.5.3

4. Use ``which python3`` to display the installation location::

	$ which python3
	/usr/local/bin/python3

Pytest 3.1.3 Installation for Python 3.5
----------------------------------------

1. Use ``pip3 install -U pytest`` to download, collect, and install pytest::

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

2. Issue the ``source`` command to reload the ``.bash_profile`` in your home directory and apply the path updates to your active shell session::

	$ source ~/.bash_profile

3. Print the installed version of pytest by using ``pytest --version``::

	$ pytest --version
	This is pytest version 3.1.3, imported from /Library/Frameworks/Python.framework/Versions/3.5/lib/python3.5/site-packages/pytest.py

..Note:: The output shows that pytest is associated with Python version 3.5. 



Pytest Software Versions
------------------------

The top output line of ``pytest`` displays the software versions that were used to process the test and in what directory::

	$ pytest
	============= test session starts ===================
	platform darwin -- Python 3.5.3, pytest-3.1.3, py-1.4.34, pluggy-0.4.0
	rootdir: /Users/McMillan/greg/uber-test, inifile:
	collected 1 item s

	test_sample.py F

	================== FAILURES =======================
	...



Cache System Files
------------------

After a test is run, two cache stores will be created inside the testing directory. See ``__pycache__`` and ``cache``::

	__pycache__/test_sample.cpython-35-PYTEST.pyc
	.cache/v/cache/lastfailed

Use these as audit logs for your tests.



Asserts for Pytests
-------------------

If an ``assert`` statement does not exist in your code, pytest will not display any assertion errors. An assert statement tells the program to test a condition and trigger an error if the condition is false.

For example, this code does not contain an assert::

	def func(x):
	    return x + 1

	def test_answer():
	    func(3) == 5

When pytest is run, no assertion error is reported::

	$ pytest test_sample.py 
	======================== test session starts =============================
	platform darwin -- Python 3.5.3, pytest-3.1.3, py-1.4.34, pluggy-0.4.0
	rootdir: /Users/McMillan/greg/uber-test, inifile:
	collected 1 item s

	test_sample.py .

	======================= 1 passed in 0.02 seconds =====================

When a ``assert`` statement is added::

	def test_answer():
	    assert func(3) == 5

The pytest displays the error::

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

Adding to this Doc Using Git
----------------------------

.. toctree::
   :depth: 1


