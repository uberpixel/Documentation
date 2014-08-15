.. _rnrecursivespinlock.rst:

******************
RecursiveSpinLock class reference
******************

.. namespace:: RN
.. class:: RecursiveSpinLock

+-------------------+---------------+
| **Availability**  | Rayne 1.0     |
+-------------------+---------------+
| **Declared in**   | RNSpinLock.h  |
+-------------------+---------------+

Overview
========

The recursive spin lock class implements a :cpp:class:`SpinLock` like class which can be locked recursively by one thread. Note that every lock has to be balanced out by one unlock.

Instance Methods
================

.. class:: RecursiveSpinLock
	
	.. function:: void Lock()

		Attempts to acquire the lock. If the lock can't be acquired, the thread will spin indefinitely until it can acquire the lock.

	.. function:: void Unlock()

		Unlocks the lock. The lock must be held by the thread.

	.. function:: bool TryLock()

		Attempts to acquire the lock. If it doesn't succeed immediately, the method will return `false`, otherwise `true`.

