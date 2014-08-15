.. _rnlockguard.rst:

****************************
LockGuard<T> class reference
****************************

.. namespace:: RN
.. class:: LockGuard

+-------------------+---------------+
| **Availability**  | Rayne 1.0     |
+-------------------+---------------+
| **Declared in**   | RNLockGuard.h |
+-------------------+---------------+

Overview
========

The LockGuard class implements general purpose lock owner that is bound to the current scope. The LockGuard will unlock the lock it's holding once it goes out of scope, wether that happens through stack unwinding during an exception throw or a normal return.
