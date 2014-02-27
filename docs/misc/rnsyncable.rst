.. _rnsyncable.rst:

************************
syncable class reference
************************

.. namespace:: RN
.. namespace:: stl
.. class:: syncable 

+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNSyncPoint.h                        |
+---------------------+--------------------------------------+
| **Namespace**       | stl                                  |
+---------------------+--------------------------------------+

Overview
========

The syncable class provides, together with the :cpp:class:`sync_point` class, an interface which allows one or more threads to synchronize with one other thread, similar to a promise/future. Unlike the former though, no data can be transferred between the threads, however, exceptions signalled via the syncable class are guaranteed to be either rethrown in a waiting thread, or, if there is no waiting thread, a rethrown within the signalling thread. This allows making waiting on a :cpp:class:`sync_point` optional while avoiding exceptions being accidentally and silently swallowed.

The syncable class is used by the thread that is doing the work that needs to be synchronized with, it allows for an arbitrary number of `sync_points` that can then wait on the syncable to be signalled. 

Instance Methods
================

.. class:: syncable

	.. function:: syncable()

		Designated constructor

	.. function:: syncable(syncable &&other)

		Move constructor

	.. function:: syncable &operator =(syncable &&other)

		Move assignment operator

	.. function:: void signal_exception(std::exception_ptr e)

		Signals the syncable, waking up all waiting threads. The exception will be rethrown in any one of the waiting threads, unless there is no waiting thread, in which case it will rethrown in the calling thread.

	.. function:: void signal()

		Signals the syncable, waking up all waiting threads.

	.. function:: sync_point get_sync_point()

		Returns a sync_point which can be used to wait on the syncable
