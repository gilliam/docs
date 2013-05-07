===========
Quick Intro
===========

In short, *Gilliam* is platform much like *Heroku*, *Google App
Engine* or *dotCloud*, but targeted against systems where the backend
is made up out of many small services (often called micro service
oriented architectures).

The main goal of Gilliam is to make it easier to develop, deploy and
scale services for these micro SOA systems. There are also a set of
secondary goals that have influenced the design:

- Few and sane dependencies
- Easy to integrate with existing systems and technoligies
- Promote best practices


Distribution and Process Model
------------------------------

In its core Gilliam is about distributing **images of software** and
making sure that a specified number of instances of each image is
executing.

The images are composed of the service, its dependencies and the full
runtime. That means that everything the service needs to run is put
into the image. There are several upsides to doing this, the main one
being that the execution environment is seperated from the hosts
system environment (e.g., operating system). This means that it is
possible to change one of them without risking to break the other one.

Even if Gilliam promotes small services there's often a need to
perform a set of different tasks.  For example, a service may want to
asynchronously do stuff in the background.  This is easiest done by
putting the job on a queue and having someone process it.  For these
reasons Gilliam have adopted `Herokus process model
<https://devcenter.heroku.com/articles/procfile>`_ where each service
(or app) can define multiple *process types*.  A **process type** is
the *execution unit and the thing that you scale*.  The process types
are defined in a file called ``Procfile`` that has content along the
following lines::

    web: python web.py
    worker: python worker.py

In the example above two process types are defined; *web* and
*worker*.  Gilliam will allow you to scale the number of processes of
each type individually.  I.e., you can have three *web* processes and
9 *worker* processes.

A service is not complete without **configuration**. Again, following
Herokus model, configuration is passed to processes via environment
variables.

**Releases** are the combination of an image and a set of
configuration variables.  Releases are immutable in the sense that to
change any of the two components a new release has to be created.

Each process of a service will be executed in an private and isolated
environment based on the image.  Currently Gilliam implements this
isolation using `LXC <http://lxc.sourceforge.net/>`_.  

The CLI Client
--------------

The way you interact with Gilliam is through a simple command line
client.  The client gives you, the developer, access to a set of tools
to deploy and scale releases of your service.

The `create` command is used to create a new service.  Creating services
are quick and cheap.  Costs come when you deploy releases::

    $ gilliam create <service name>

That's pretty much it.  The client will associate the current
directory with the created service (using the `.gilliam.app` file), so
its wise to run the command in the root directory of your service.

In the following sections we will contain more information about
different commands that the client provides.

Deploying
---------

Gilliam comes with a build server that takes your service code and
packages it into an image. Like many Platform as a Service options,
the client is integrated with *git*, allowing you simply build and
deploy the *HEAD* of your git repository::

    $ gilliam deploy

This command will push the contents of your git repository to the
build server which will bundle it with the runtime and dependencies
into an image that will then be released.

It is worth noting that processes will not start executing just
because you ran the `deploy` command and created a release. For this
to happen, scale factors has to be set for the release. More on that
in the section on scaling.

Configuration
-------------

Configuration is controlled using the `config` command in the client.
To display the current configuration, just run the command without
any arguments::

    $ gilliam config
    POOL_SIZE=32

Changing the configuraton is a simple as specifying the new values 
when executing the `config` command::

    $ gillam config POOL_SIZE=64
    v2 releases

As you can see from the output a new release was created by the
configuration change.

Scaling
-------

To get something to actually execute from a release scaling factors
need to be set for that release.  This is done using the `scale`
command. *Scaling factors* are the desired state that you want
Gilliam to maintain.  The factors are set on a per-process type
basis.  Given the example *Procfile* in the introduction, to get
two web processes and four worker processes running run the
following command::

    $ gilliam scale v2 web=2 worker=4

It is possible to inspect current scaling factors by not specifying
any new ones::

    $ gilliam scale
    v2 web=2 worker=4

It might take Gilliam a few seconds to react to the changes to the
scaling factors, but when it does you may see the created processes
using the `ps` command::

    $ gilliam ps
    web.1 v2 state running (just now) on host H port 10000
    web.2 v2 state running (just now) on host H port 10001

