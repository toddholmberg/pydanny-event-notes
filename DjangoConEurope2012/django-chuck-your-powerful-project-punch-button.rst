============================================================
Django Chuck - Your powerful project punch button
============================================================

by Bastian Ballmann and Lukas Bünger

.. note:: Looks to be an amazing, modular tool for standing up projects easily. Missed most of the talk so my notes are incomplete.

Why the name Chuck?
========================

* Chuck is not informal term for meal
* Not meaning vomit
* Chuck has no times to anything

Use case for django-chuck
====================================

* Same setup all the time
* Manual project setups
* Same conditions apply all the time

Why not Pinax?
==============

* No modular template structure or code base
* Monolithic Python script
* Addresses project creation only
* No flexible build process management

Installation
================

.. parsed-literal::

    pip install django-chuck
    
copy example_conf.py to:

    ~/django_chuck_conf.py
    
See django-chuck.rtfd.org

Example usage
==============

.. parsed-literal::

    chuck create_project <prefix> <name> [modules] -a [pip modules]
    chuck create_project ni djangocon django-cms,test,nginx
    
What happened?
===============

This got generated:

* settings
* requirements
* uwsgi
* fabfile
* hosting
* jenkins
* templates

Setup an existing project from source
========================================

.. parsed-literal::

    chuck setup_project git@whatever.com:your-project.git
    
.. note:: Stepped away for things. 