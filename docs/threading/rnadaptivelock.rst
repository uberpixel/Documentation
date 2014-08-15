.. _rnadaptivelock.rst:

******************
AdapativeLock class reference
******************

.. namespace:: RN
.. class:: AdapativeLock

+------------------+-------------------+
| **Availability** |     Rayne 1.0     |
+------------------+-------------------+
| **Declared in**  | RNAdapativeLock.h |
+------------------+-------------------+

Overview
========

The AdapativeLock class implements an adaptive lock that bridges the gap between :cpp:class:`SpinLock` and :cpp:class:`Lock`. It is implemented as a basic spin lock where the waiting thread is spun for some time period when already held by another thread, if the lock can't be acquired, the thread is put on the waiter list and send to sleep. This lock type works best for low to medium contention.

Instance Methods
================

.. class:: AdapativeLock
	
	.. function:: void Lock()

		Attempts to acquire the lock. If the lock can't be acquired immediately, the thread will spin for some time until it gives up and yields up all CPU time until the lock can be acquired.

	.. function:: void Unlock()

		Unlocks the lock. The lock must be held by the thread.

	.. function:: bool TryLock()

		Attempts to acquire the lock. If it doesn't succeed immediately, the method will return `false`, otherwise `true`.

