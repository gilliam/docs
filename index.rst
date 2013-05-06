.. Gilliam documentation master file, created by
   sphinx-quickstart on Wed Feb  6 19:56:39 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Gilliam
==================

Gilliam is a platform for hosting what is called `12 factor
<http://www.12factor.net>`_ apps.  It aims to make the live easier for
developers of micro service oriented architectures.

Gilliam does this by providing isolated environments where your
services run, a simple build sever that packages your service into
artifacts that can quickly be deployed and a scheduler that makes sure
your services keep running in the case of failure.

You can find Gilliam at `Github <http://github.com/gilliam>`_.


Distribution
------------

The platform is responsible for making sure that services are running
at all times.  The platform should also make sure that service
instances are placed to minimize the effect of failures.  Gilliam does
this by having the user specify a scaling factor for a release.  This
scaling factor states the desired number of instances per process
type.  It is up to the platform to constantly monitor and make sure
that enough resources are allocated to meet the requirements.

Distribution is implemented in the `scheduler
<http://github.com/gilliam/scheduler>`_.


Releases
--------

The platform bundles software with its runtime and dependencies into
an image.  When this image is combined with configuration a release is
formed.  Releases are immutable once they have been created.  If config
is changed, a new release has to be done.

Releases are also the unit of scaling, allowing a sevice to have
multiple releases running at the same time.


Isolation
---------

Services instances are isolateed from other instances of the same
service, and from instances of other services.  Each instance has a
private execution environment and a limited set of CPU and memory
resources.  The execution environment is completely isolated from the
hosts execution environment, allowing changes and upgrades of the host
without risking to affect the services.

Gilliam can be adopted to use different kinds of isolation or
virtualization techniques, but uses LXC as default.


Configuration
-------------

Config is what changes between stages (testing, staging, production,
different sites). The service gets its configuration from the platform
in the form of values in environment variables.


Polyglot
--------

The platform supports services written in any language, as long as
there is a way to build an image of it.  Since the runtime is bundled
with the image the platform will allow hetrogenous installations even
within a single service.


Integration
-----------

One of the goals of Gilliam is that it must be easy to integrate into
existing environment.  There for, a lot of the "magic" is implemented
using shell scripts, separated from the distribution logic.


Ancillary Services
------------------

Not yet supported, but Gilliam will at some point support simple
provisioning of ancillary services such as databases, caches and queues. 


Table of Content
================

.. toctree::
   :maxdepth: 2

   requirements
   install


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

