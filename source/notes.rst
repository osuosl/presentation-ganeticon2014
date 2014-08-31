Notes
=====

(Lance) [user presentation 45min]
---------------------------------

Developing Ganeti Web Manager is difficult to do when several developers need to
have access to a test Ganeti environment.  We've been using a Vagrant+Puppet
environment which compiles the version of Ganeti they need. However, given the
increase in Haskell dependencies this has become increasing difficult to do. So
we've been taking a look at using Omnibus from Chef Inc to build an all-in-one
binary package for testing purposes. We'll talk about the challenges of using
Omnibus and the pros/cons of it as well.  Along with a Chef cookbook we've been
developing for deploying Ganeti.

(Lance & Ken) [design discussion 1hr]
-------------------------------------

Part of the Ganeti Web Manager redesign is to basically create a layer in front
of Ganeti to deal with users, permissions and quotas. We've been using Openstack
quite a bit lately and have found that their frontend, Horizon might be a great
fit for a new frontend for Ganeti. We we'd like to potentially discuss is
specific features that might make the new backend of Ganeti Web Manager work
more smoothly with Ganeti itself.  There might be some overlap with synnefo so
it would be interesting to discuss this with that team as well.
