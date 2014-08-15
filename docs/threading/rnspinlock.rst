.. _rnspinlock.rst:

******************
SpinLock class reference
******************

.. namespace:: RN
.. class:: SpinLock

+------------------+--------------+
| **Availability** |  Rayne 1.0   |
+------------------+--------------+
| **Declared in**  | RNSpinLock.h |
+------------------+--------------+

Overview
========

The SpinLock class implements the most lightweight locking mechanism in Rayne. It works completely in userspace works best in cases with very little contention or when the lock is only held for a very short period of time. If the lock can't be acquired, the waiting thread will spin until it can acquire the lock.

Instance Methods
================

.. class:: SpinLock
	
	.. function:: void Lock()

		Attempts to acquire the lock. If the lock can't be acquired, the thread will spin indefinitely until it can acquire the lock.

	.. function:: void Unlock()

		Unlocks the lock. The lock must be held by the thread.

	.. function:: bool TryLock()

		Attempts to acquire the lock. If it doesn't succeed immediately, the method will return `false`, otherwise `true`.

