.. _rnsyncpoint.rst:

**************************
sync_point class reference
**************************

.. namespace:: RN
.. namespace:: stl
.. class:: sync_point 

+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNSyncPoint.h                        |
+---------------------+--------------------------------------+
| **Namespace**       | stl                                  |
+---------------------+--------------------------------------+

Overview
========

The sync_point class is the counter part to the :cpp:class:`syncable` class, and allows a thread to synchronize with the associated syncable.

Instance Methods
================

.. class:: sync_point

	.. function:: sync_point()

		Designated constructor. The created sync_point is marked as already signalled and has no syncable associated with it.

	.. function:: sync_point(sync_point &&other)

		Move constructor

	.. function:: sync_point &operator =(sync_point &&other)

		Move assignment operator

	.. function:: void wait()

		Waits for the associated syncable to be signalled. If the syncable has already been signalled, this method is effectively a no-op. If the syncable signals an exception, the exception will be rethrown on the waiting thread.

	.. function:: bool signalled()

		Returns true if the associated syncable has already been signalled.
		