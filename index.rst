.. Gilliam documentation master file, created by
   sphinx-quickstart on Wed Feb  6 19:56:39 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Gilliam
==================

In short, *Gilliam* is platform much like *Heroku*, *Google App
Engine* or *dotCloud*, but targeted against systems where the backend
is made up out of many small services (often called micro service
oriented architectures).

Gilliam does this by providing isolated environments where your
services run, a simple build sever that packages your service into
artifacts that can quickly be deployed and a scheduler that makes sure
your services keep running in the case of failure.

You can find Gilliam at `Github <http://github.com/gilliam>`_.

The services running on top of Gilliam are built using the
`twelve-factor methodology <http://www.12factor.net>`_ (if you read
this a lot of things about Gilliam will make more sense).

Table of Content
================

.. toctree::
   :maxdepth: 2

   quick-intro
   requirements
   install


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

