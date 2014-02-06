.. _rnringbuffer.rst:

***************************
ring_buffer class reference
***************************

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

	.. function:: size_type size() const

		Returns the size of the receiver

	.. function:: void push(const_reference& value)

		Copies the value to the end of the receiver, potentially overriding the beginning

	.. function:: void push(value_type&& value)

		Moves the value to the end of the receiver, potentially overriding the beginning

	.. function:: void pop()

		Removes the value at the beginning of the receiver

	.. function:: reference operator [](size_type index)

		Returns the element at the given index, where index 0 is the first element in the receiver

	.. function:: const_reference operator [](size_type index) const

		Returns the element at the given index, where index 0 is the first element in the receiver

	.. function:: reference at(size_type index)

		Returns the element at the given index, where index 0 is the first element in the receiver

	.. function:: const reference at(size_type index) const

		Returns the element at the given index, where index 0 is the first element in the receiver

	.. function:: reference front()

		Returns the first element in the receiver

	.. function:: const_reference back() const

		Returns the last element in the receiver

	.. function:: reference back()

		Returns the last element in the receiver

	.. function:: const_reference back() const

		Returns the last element in the receiver

	.. function:: iterator begin()

		Returns an bidirectional iterator to the first element. 

		.. note:: that iterators don't consume the elements in the ringbuffer, ie, they are still in the ringbuffer

	.. function:: const_iterator begin() const

		Returns an bidirectional const iterator to the first element. 

		.. note:: that iterators don't consume the elements in the ringbuffer, ie, they are still in the ringbuffer

	.. function:: iterator end()

		Returns a bidirectional iterator to the element one past the last element. Even though this is an iterator to a ringbuffer, the returned iterator will point to an invalid element.

	.. function:: const_iterator end()

		Returns a bidirectional const iterator to the element one past the last element. Even though this is an iterator to a ringbuffer, the returned iterator will point to an invalid element.
