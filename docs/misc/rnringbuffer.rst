.. _rnlockfreeringbuffer.rst

*********************
ring_buffer class reference
*********************

.. namespace:: RN
.. namespace:: stl
.. class:: ring_buffer 

+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNRingbuffer.h                       |
+---------------------+--------------------------------------+
| **Namespace**       | stl                                  |
+---------------------+--------------------------------------+

Overview
========

The ring_buffer class implements an allocator aware, stl compatible ring buffer with support for bidirectional iterators. Although they can't be resized after construction, their capacity doesn't have to be known at compile time. Unlike its counterpart, :cpp:class:`lock_free_ring_buffer`, the ring_buffer won't protect your data from being overridden once its size reached the maximum capacity, so you have to add checks to your code if you need to protect your data.
 

Instance Methods
================

.. class:: ring_buffer

	.. function:: size_type capacity() const

		Returns the maximum capacity of the receiver.

	.. function:: bool push(T&& value)

		Attempts to insert the given value into the receiver. If the operation fails because the receiver was already full, the operation will return `false` and no state is changed.

	.. function:: bool pop(T& value)

		Attempts to move the first un-read value from the receiver into value. If the receiver was empty, the method will return `false` and the passed value is not altered in any way.

	.. function:: bool was_empty() const

		Returns `true` if the receiver was empty when the operation ran.

	.. function:: bool is_lock_free() const

		Due to C++11's `std::atomic<>` behaviours, it is not guaranteed that a given implementation uses atomic instructions found in the targeted CPU or if it internally uses locks to guarantee atomicity. All modern CPUs and compiler should support creating lock free `std::atomic<size_t>` instances and this method should return always `true` on all targets.
		