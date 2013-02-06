.. Gilliam documentation master file, created by
   sphinx-quickstart on Wed Feb  6 19:56:39 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Gilliam's documentation!
===================================

This is the documentation for Gilliam, a simple app hosting platform.

Contents:

.. toctree::
   :maxdepth: 2

What is it?
-----------

Gilliam is a platform for hosting what is called *12 factor* apps.  It
aims to make the live easier for developers and operators of
distributed systems.  It also helps you with continious deployment.

Gilliam does this by providing isolated environments where your apps
run, a simple build sever that packages your apps into artifacts that
can quickly be deployed and an orchestrator that makes sure your apps
keep running in the case of failure.


Requirements
------------

Operating System

* Ubuntu 12.04 LTS

Python

* Python 2.7
* Routes
* glock
* WebOb
* docopt
* storm
* requests
* shortuuid

In general, see ``requirements.txt`` in each project.

Currently Gilliam only comes with database schemas for SQLite3, but
Storm supports Postgres and MySQL so it should be trivial to port to
those database systems.

Install
-------

Setup
-----


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

