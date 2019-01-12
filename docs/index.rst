.. simple_email documentation master file, created by
   sphinx-quickstart on Fri Oct 19 11:15:29 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Bulwark's Documentation
========================================

Bulwark is a package for convenient property-based testing of pandas dataframes, supported for Python 3.5+.

This project was heavily influenced by the no-longer-supported `Engarde`_. library
by Tom Augspurger (thanks for the head start, Tom!), which in term was modeled after
the R library `assertr`_.

.. _Engarde: https://github.com/TomAugspurger/engarde
.. _assertr: https://github.com/ropenscilabs/assertr


Why?
====

Data are messy, and pandas is one of the go-to libraries for analyzing tabular data.
In the real world, data analysts and scientists often feel like they don't have the time
or energy to think of and write tests for their data. Bulwark's goal is to let you check
that your data meets your assumptions of what it should look like at any (and every) step
in your code, without making you work too hard.


Usage
=====

Bulwark comes with checks for many of the common assumptions you might want to validate
for the functions that make up your ETL pipeline, and lets you toss those checks as decorators
on the functions you're already writing:

.. code-block:: python
   import bulwark.decorators as dc

   @dc.is_shape(-1, 10)
   @dc.is_monotonic(strict=True)
   @dc.none_missing()
   def compute(df):
       # complex operations to determine result
       ...
       return result_df

Still want to have more robust test files? Bulwark's got you covered there, too, with importable functions.

.. code-block:: python
   import bulwark.checks as ck

   df.pipe(ck.none_missing())
   

Won't I have to go clean up all those decorators when I'm ready to go to production?
Nope - just toggle the built-in debug_mode flag available for every decorator.

.. code-block:: python
   @dc.is_shape((3, 2), debug_mode=False)
   def compute(df):
       # complex operations to determine result
       ...
       return result_df

What if the test I want isn't part of the library?
Use the build-in `verify`, `verify_all`, `veryify_any` functions/decorators to use your own
custom function!

.. code-block:: python
   def custom_check_func(df):
       # some really special check
       ...
       return df

   @dc.verify_all(custom_check_func)
   def compute():
       # complex operations to determine result
       ...
       return result_df

Check out :ref:`examples` to see more advanced usage.


Contents
========

.. toctree::
   :hidden:
   
   installation
   quickstart
   design
   examples
   api
   contributing