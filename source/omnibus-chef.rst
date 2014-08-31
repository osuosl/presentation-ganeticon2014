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


