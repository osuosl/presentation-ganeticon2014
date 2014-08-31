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

* Use Ganeti PPA / JFut's YUM repo
* Build our own deb/rpms
* Omnibus binary package

Omnibus Intro
-------------

* Full-stack Project Installer
* Vendorize all dependencies into a single binary rpm/deb
* Chef, Chef-Server, Chef-DK uses Omnibus

Omnibus Pros/Cons
-----------------

:Pros:

  * Complete control of the whole software stack dependency tree
  * No distro-specific package dependencies
  * Single Package to install

:Cons:

  * Prefix hell
  * Security maintenance for all libraries
  * Build caching with git
  * Building large packages can be complicated

How Omnibus Works
-----------------

* Builds a self contained prefixed environment on the host machine
* Typically built using Test Kitchen on a target OS Virtual machine
* Installs and creates a sane build environment
* Installs Omnibus project configuration
* Runs omnibus to install the project
* Uses git and git tags to cache builds
* Ensures no external library linking

So why use Omnibus for Ganeti?
------------------------------

* Curious if it would work!
* Build Ganeti with the upstream preferred versions of libraries
* Automate builds for testing of GWM
* Seemed like an interesting way to package Ganeti in an easy form

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

Cookbook TODOs
--------------

* Support for Debian 7 and Ubuntu 14.04
* Installing using Omnibus Ganeti
* Publish Ganeti Instance Image cookbook
* Xen Support
* Internal wrapper cookbook for site specific needs

Questions?
==========

:name: Lance Albertson
:company: OSU Open Source Lab
:email: lance@osuosl.org
:twitter: @ramereth @osuosl

*Attribution-ShareAlike CC BY-SA ©2014*

