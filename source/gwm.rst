==================
Ganeti Web Manager
==================

Cluster Management Made Simple


Kenneth Lett
OSU Open Source Lab


Who are we?
===========

**OSU Open Source Lab**

- We provide infrastructure and hosting for Open Source Projects
- We foster and develop Open Source software
- We are from Oregon

How do we use Ganeti
====================

- Ganeti Instance Image
- Primary prod cluster

  - 6 nodes, 147 instances
- Project clusters (i.e. PSF, OSGeo, etc)
- Host mail servers, websites, etc

What is GWM?
============

**Easy to use Web interface to Ganeti**

.. rst-class:: build

- Make everything visible
- Client-facing interface
- Leverage all of Ganeti's features via RAPI
- Provide granular permissions
- Organize users arbitrarily
- Make management easy with templates and bulk actions

.. note::

    Quick overview for those who aren't familiar, this is a list of
    goals for the project.


GWM Structure
=============

.. rst-class:: build

- Django web framework
- JQuery
- Open Sourced Components
- Django Object Permissions
- Django Object Log
- NoVNC

.. note::

    Skip through quickly, point out recent work with NoVnc


GWM Structure
=============

.. rst-class:: build

- User/Group structure determines authorization and ownership
- Models encapsulate persistent data for clusters and instances
- Changes to the models are communicated to Ganeti as jobs
- Cache system updates models from current Ganeti state

.. note::

    Skip through quickly


GWM Structure
=============

Caching cluster information to avoid frequent API calls

.. figure:: /_static/ganeti_cache.png
    :align: center

.. note::

    Note the reliance on the RAPI and how the design was informed by the RAPI's
    performance. Faster RAPI means less need for heavy caching


GWM Structure
=============

- NoVNC provides console access from the web interface
- VNC Auth proxy allows access to a VNC terminal on instances from the web client 

.. figure:: /_static/vnc1.png
    :align: center

.. note::

    NoVNC is a bit of a moving target, as is websockets support
    Note work towards a more general proxy for both serial and vnc connectivity


New in 0.11
===========

**Stabilize and Package**

.. rst-class:: build

- Move to Github
- Modularization
- Setup script (GSoC project)
- Python package
- Development Environment (vagrant)
- Better documentation
- Chef deployment (Work in progress)

.. note::

    :Github:
      - more visibility, easier contribution
      - pull requests are more familiar to many new developers

    :Modularization:
      - split out the functional units, easier to maintain, add new apps

    :Setup script:
      - simplified installation
      - useful for creating the python package
      - scripts both dev and production setup steps

    :Python package:
      - standardized installation for python applications
      - easier deployment, automated and manual

    :Dev env:
      - vagrant environment with chef to deploy
      - deploy to any vagrant provider, virtualbox, openstack, etc

    :Docs:
      - complete restructure of documentation
      - prototype documentation for other OSL projects
      - community-oriented contributor docs

    :Chef deployment:
      - setup scripts, vncauthproxy init script, and other components
      - Automate the whole deployment, still a WIP

New in 0.11
===========

**New Features**

.. rst-class:: build

- VM creation wizard
- Bulk actions
- Visualization

.. note::

    :Wizard:
      - makes VM form a logical workflow
      - replaces very large, unmaintainable javascript
      - uses standard Django form wizard and methodology
      - easy to save as template

    :Bulk actions:
      - ability to select multiple VMs for certain actions (not all implemented
        yet)

    :Visualization:
      - GSOC project provides a javascript visualization of cluster - can be
        expanded into an admin interface


Experimental Projects
=====================


.. rst-class:: build

- Export VM
- Serial Console
- Omnibus packaging
- Horizon Ganeti (Design discussion)

  .. figure:: _static/openstack-screenshot.png
      :align: center
      :scale: 90%

.. note::

    These items are not complete, but have been experimented with (Lance input?)

    :Export: use ganeti's export functionality to export vms via GWM/RAPI

    :Serial Console:
      direct connection to hypervisor serial console using an authproxy similar
      to vncauthproxy, and socat. Very difficult, some progress using Twisted
      and websockets, but not finished before 0.11. This is an important
      functionality for GWM's future

    :Omnibus Packaging:
      Single RPM/DEB installation with all requirements. Very Experimental.

    :Horizon Ganeti:
      Utilizing the webgui in Horizon instead of writing our own. Basics working
      talking directly to cluster.

Lessons Learned
===============

.. rst-class:: build

- Serial terminal communication
- Django packaging
- Ganeti RAPI Documentation

Future Plans
============

|

.. figure:: /_static/the_general_problem.png
    :align: center


GWM API
=======

.. rst-class:: build

- Rest API layer between Ganeti RAPI and user interface
- Implement core GWM functions, user/group management, quotas, VNC and Serial consoles
- Allow multiple front-end interfaces, Horizon, mobile apps, etc
- Leverage third party authentication tools
- Use external job queue and caching systems

.. note::

    We'll discuss the details of the redesign in Thursday's design talk
    Live demo of GWM if time and interest


GWM API
=======

.. figure:: /_static/diagram.png
    :align: center

Ganeti at OSL Status Report
===========================

- Not much has changed since last year
- Still running 2.6.2 :(
- Still migrating hosts from Gentoo to CentOS 6
- Consolidating project clusters
- Working on a Chef Cookbook
- Ganeti/Openstack integration ideas

Questions?
==========


:author: Ken Lett, Lance Albertson
:email: kennric@osuosl.org, lance@osuosl.org
:twitter: kennric, @kenlett, @ramereth
:sites: http://code.google.com/p/ganeti/,
  http://code.osuosl.org/projects/ganeti-webmgr
:irc: #ganeti-webmgr, #osuosl
