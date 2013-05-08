.. Gilliam documentation master file, created by
   sphinx-quickstart on Wed Feb  6 19:56:39 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Gilliam
==================

*Gilliam* is a platform for `micro service architecturs
<http://yobriefca.se/blog/2013/04/29/micro-service-architecture/>`_
and `12 factor <http://www.12factor.net>`_ apps.

Gilliam runs your services in isolated environments using
LXC. It comes with a simple build server that packages your service
into an artifact that can quickly be deployed. The core component of
Gilliam is the scheduler, which is responsible for making sure that
your services are always running.

Heroku and other platform as a services have been big sources of
inspiration for Gilliam. If you read about the `twelve-factor
methodology <http://www.12factor.net>`_ a lot more things about
Gilliam will make sense.

You can find Gilliam at `Github <http://github.com/gilliam>`_.


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

