.. _rnlockfreeringbuffer.rst:

**********************************************
lock_free_ring_buffer<T, Size> class reference
**********************************************

.. namespace:: RN
.. namespace:: stl
.. class:: lock_free_ring_buffer<T, Size> 

+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNRingbuffer.h                       |
+---------------------+--------------------------------------+
| **Namespace**       | stl                                  |
+---------------------+--------------------------------------+

Overview
========

The lock_free_ring_buffer<T, Size> class implements a thread safe single-reader/writer ring buffer that doesn't use locks for synchronization. Unlike it's non-thread safe counterpart :cpp:class:`ring_buffer<T>`, it doesn't support STL features like iterators and overriding entries that haven't been read yet. For performance reasons, storage can't be resized at runtime and the capacity must be known at compile time.
 

Instance Methods
================

.. class:: lock_free_ring_buffer<T, Size>

	.. function:: bool push(const T& value)

		Attempts to insert the given value into the receiver. If the operation fails because the receiver was already full, the operation will return `false` and no state is changed.

	.. function:: bool push(T&& value)

		Attempts to insert the given value into the receiver. If the operation fails because the receiver was already full, the operation will return `false` and no state is changed.

	.. function:: bool pop(T& value)

		Attempts to move the first un-read value from the receiver into value. If the receiver was empty, the method will return `false` and the passed value is not altered in any way.

	.. function:: bool was_empty() const

		Returns `true` if the receiver was empty when the operation ran.

	.. function:: bool is_lock_free() const

		Due to C++11's `std::atomic<>` behaviours, it is not guaranteed that a given implementation uses atomic instructions found in the targeted CPU or if it internally uses locks to guarantee atomicity. All modern CPUs and compiler should support creating lock free `std::atomic<size_t>` instances and this method should return always `true` on all targets.
		