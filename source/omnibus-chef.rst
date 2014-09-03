Omnibus and Chef with Ganeti
============================

:authors: Lance Albertson
:title: Director
:company: OSU Open Source Lab
:email: lance@osuosl.org
:twitter: @ramereth

Summary
-------

* GWM Development Current Environment
* Current challenges
* Omnibus introduction
* Pros/Cons
* Challenges
* Demo
* Chef and Ganeti
* Cookbook Overview

Current GWM Dev Environment
---------------------------

* Vagrant + Puppet (3 nodes)
* Prepackaged Vagrant Boxes
* Ganeti compiled from source
* Very specific Puppet module
* Supports various platforms
* Removes the need for hardware clusters for testing

Challenges with current system
------------------------------
* Compile requirements for Ganeti have increased

  * Additional Haskell dependencies require more RAM to link
  * Increased time to redeploy test environment
* Difficult to maintain
* Building from source is problematic, increases installation dependencies
* Difficult to keep up to date with upstream changes
* Difficult to adjust cluster configuration
* Puppet module not meant to be run in production

Build environment requirements
------------------------------

* Deploy any (reasonable) version of Ganeti

  * Most current, A few older versions, master/develop branches
* Flexible enough to deploy a variety of cluster environment configurations

  * DRBD/Plain/File
  * RDB/Ceph/Gluster
  * Varying OS Definitions
* Support various OS host platforms: Debian, Ubuntu and CentOS

Ganeti Installation Options
---------------------------

Packaging with current Ganeti releases:

:Debian: Backports
:Ubuntu: Ganeti PPA
:RHEL: JFut's yum repo

Other Options:

.. rst-class:: build

* Build our own deb/rpms
* Build from source
* Omnibus binary package

Reasons for try Omnibus
-----------------------

- The Challenge -- will it work?
- Study the feasibility given Ganeti's growing dependencies
- Research the pros/cons of the method
- Its fun, right? :)

So what is Omnibus?
-------------------

* Full-stack Project Installer
* Vendorize all dependencies into a single binary rpm/deb

  - All software dependencies are build into a prefixed environment
    ``/opt/ganeti``
  - Only system libraries are allowed to be linked to software (i.e. glibc, etc)
* Chef, Chef-Server, Chef-DK uses Omnibus

Omnibus Pros
------------

* Complete control of the whole software stack dependency tree
* Use newer versions of software that upstream prefers
* No distro-specific package dependencies
* Build caching with git
* Single Package to install
* Extremely simple installation and deployment

Omnibus Cons
------------

* Prefix hell

  - Making sure everything is linked to the prefix environment
  - Fixed path assumptions by upstream (i.e. ``/usr/bin/python``)
* Security maintenance for all software (yes, you even build your own openssl)
* Building large packages can be complicated
* Non-standard method

How Omnibus Works
-----------------

* Builds a self contained prefixed environment on the host machine
* Typically built using Test Kitchen/Vagrant on a target OS Virtual machine
* Installs and creates a sane build environment
* Installs Omnibus project configuration
* Runs omnibus to install the project
* Installs package dependencies
* Ensures no external library linking
* Exports a deb/rpm at the end

Demo
----

.. code-block:: bash

  # CentOS 6
  yum install http://ftp.osuosl.org/pub/osl/omnibus/ganeti/ganeti-2.11.2_20140704_192212-1.el6.x86_64.rpm

  # Ubuntu 12.04
  wget http://ftp.osuosl.org/pub/osl/omnibus/ganeti/ganeti_2.11.2-20140704-192150-1_amd64.deb
  dpkg -i ganeti_2.11.2-20140704-192150-1_amd64.deb

  # Debian 7
  wget http://ftp.osuosl.org/pub/osl/omnibus/ganeti/ganeti_2.11.2-20140704-191038-1_amd64.deb
  dpkg -i ganeti_2.11.2-20140704-191038-1_amd64.deb

How its built
-------------

https://github.com/osuosl/omnibus-ganeti

* Everything is installed into ``/opt/ganeti``
* Binaries and libraries are in ``/opt/ganeti/embedded``
* Post-install hooks setup symlinks to ``/usr/sbin``, etc
* GHC installed from distro
* Haskell deps installed via cabal
* Python deps installed via pip
* Currently only tarball installs work

  * Having issues with pandoc with git builds

Problems I ran into
-------------------

:Haskell:
  * Requires GHC installed from Distro
  * Cabal dependency hell!
  * Cabal version issues (CentOS vs. Ubuntu/Debian)
  * ``RPATH`` not being set correctly
  * ``Werror`` Issues
  * GMP Version issues
:Python:
  * Hard coded ``/usr/bin/python`` paths in Ganeti

Chef and Ganeti
===============

Cooking up some Ganeti awesome!

Ganeti Cookbook
---------------

https://github.com/osuosl-cookbooks/ganeti

* Currently supports CentOS 6 and Ubuntu 12.04
* Installs Ganeti from Ubuntu PPA or JFut's Yum repo
* Ganeti initialization support
* Setting of RAPI users via encrypted data bags
* Demo

Cookbook TODOs
--------------

* Support for Debian 7 and Ubuntu 14.04
* Installing using Omnibus Ganeti
* Publish Ganeti Instance Image cookbook
* Xen Support ?
* Internal wrapper cookbook for site specific needs

Questions?
==========

:name: Lance Albertson
:company: OSU Open Source Lab
:email: lance@osuosl.org
:twitter: @ramereth @osuosl

*Attribution-ShareAlike CC BY-SA ©2014*

