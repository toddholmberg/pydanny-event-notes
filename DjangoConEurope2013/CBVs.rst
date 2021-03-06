=======================================
Class Based Views: Untangling the Mess
=======================================

by Dr. Russell Keith-Magee

    * Django Core Developer since January 2006
    * DSF President since June 2010
    * CTO and co-founder of TradesCloud

Why CBVs?
============

Introduced in Django 1.3 in 2011. What's the history?


History per 2005
-------------------

* Django is for building websites
* Views are for displaying content
* There are lots of refactorable things to do
* Generic views could handle all of this:

    * Display template
    * Display object or list of objects
    * Handle forms
    * Every view is a function
    * Configuration via arguments
    
Problems with function based generic views
------------------------------------------

* Configuration options limited by urls.py args
* No control over logic flow
* No re-use between views

.. warning:: Another thing against function-based generic views was that people can and do implement their own broken CBV system. Leaky states is a serious issue. Don't roll your own unless you really understand 

Django 1.3
-----------

* They kept trying to get CBVs into Django starting with Django 1.0.

What went wrong
=================

* Fundamental confusion over purpose
* Confusion over implementation choices
* Ravioli code

    * Luke Plant described the effort as bad code.
    * "You don't know what's in the ravioli."
    * Steep learning curve

* Bad documentation

    * Russell takes the blame for the problems.
    * Myself, Marc Tamlyn, and others worked to make it work.
    
Purpose
----------

Class-Based views are an object-oriented analog for function based views.

* Class based views
* Class based Generic Views

Because we are subclassing a base class, we get tons of extra options.

* automatic OPTIONS request handling
* automatic naive HEAD request handling
* automatic HTTP 405 on unknown verbs

CB Generic Views
~~~~~~~~~~~~~~~~~~~

* Uses Class Based Views as a base
* Creates analogs of the old generic views
* Addresses limits of functional approach

Implementation Choices
--------------------------

* See details of the debate at https://code.djangoproject.com/wiki/ClassBasedViews
* A class that is instantiated as a view
* Problems:

    * What gets instantiated?
    * How does it gets instantiated?
    * Once per process or request?
    * What's the lifespan?
    * What about state? (race conditions!!!)
    * How does it work with ``urls.py``?
    * How do you configure things?
    
* Django's admin system is a CBV

    * Implemented using simple ``__call__()``
    * Doesn't have HTTP Verb support
    * Suffers from serious state issues

.. warning:: Don't put ``self`` on Django admin objects or you will cause state issues.

Other concept design:

    * Change the ``urls.py`` contract

        * Current: a callable
        * Change to: A callable or a class
        * The problem is that this would have forced them to change a lot of source code and make things under the hood much more complex.
        
    * Decision: keep the ``urls.py`` contract clear
    
Ravioli
------------

* Goal: Replace FBV generics with CBV generics
* Make it easy to extend
* Unfortunately complex class hierarchy
* However...

    * Allows for maximum reuse of core logic
    * Extremely flexible for inserting new logic
    * Easy to add your own mixins

Documentation
-----------------

* Bad as originally designed
* Much better now
* Still need framework decisions needed

.. note:: Use django-braces to fill out the missing pieces of CBVs.

Where to from here?
=====================

* Add new features?
* Did they solve the wrong problem? Modern problems:

    * Multiple forms/formsets per page
    * Conditional forms
    * Continuous scrolling, not pagination
    * AHAX support
    * PJAX
    * Multiple "actions" per page

Call to Action
================

* IN discussion: Do you mean CBV or CBGV?
* Docs can still be improved. YESSS!!!!
* #18830 - FormCollection
* Experiment with APIs. Django's admin is a useful case study

Documentation Ideas for CBVs during the sprints
================================================

.. note:: I'm not working on Django CBV documentation during the sprints. However, I'm open to suggesting paths to take:

* Tutorials in the CBVs section of the core Django documents.
* More working code examples
* Flow charts!
