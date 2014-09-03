========================
OSUOSL Design Discussion
========================

:authors: Lance Albertson, Ken Lett
:company: OSU Open Source Lab
:email: lance@osuosl.org, kennric@osuosl.org

Overview
========


.. figure:: /_static/rtfm.png
    :align: center

.. note::

    We recognize that many of the features we'd like to see may already be implemented, or might be implementable with existing features. This requires that the documentation be good enough to discover...

Overview
========


.. figure:: /_static/hell.png
    :align: center

.. note::

    And we also want to be careful that we are not asking for accommodation of our square peg into a round solution

Overview
========

**It's all about the RAPI**

- RAPI Documentation
- RAPI Performance
- Third Party Design Considerations
- Extras


RAPI Documentation
==================

- Documented return status, http status, etc
- API versioning

.. note::

    :documentation: Maybe auto-doc of some kind? Need all possible return values, http codes, etc
    :versioning: Does it have to track ganeti major version? What is the update plan?


RAPI Perfomance
===============

**Goals**
- Minimize the difference between Ganeti's state and our knowledge of Ganeti's state
- Avoid waiting around for Ganeti


.. rst-class:: build

- Fast access to cluster and instance state
- Slower access to cluster and instance details
- Feedback: Is my VM ready yet?
    

RAPI Performance
================

.. rst-class:: build

- Cache state in memory for fast access?
- Optimized status endpoints?
- Separate metadata daemon/API


RAPI Job/Status Tracking
========================

.. rst-class:: build

- /jobs/<id>/wait
- Polling
- Watcher daemon
- Central reporting
- Callback URL

.. note::

    :wait: - not well documented, how long does it wait?


Third Party Design Considerations
=================================

- API design - converging on Openstack?


Extras
======

- Authorization setup via RAPI
- Log / Job history access


Discussion
==========

*Attribution-ShareAlike CC BY-SA ©2014*

