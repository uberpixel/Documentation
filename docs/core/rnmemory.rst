.. _rnmemory.rst:

**************************
Memory functions reference
**************************

.. namespace:: RN
.. namespace:: Memory

+------------------+------------+
| **Availability** | Rayne 1.0  |
+------------------+------------+
| **Declared in**  | RNMemory.h |
+------------------+------------+
| **Namespace**    | Memory     |
+------------------+------------+ 

Overview
========

Because of Raynes demands on high performance across multiple threads, memory in Rayne is backed by tcmalloc/gperftools. Unlike the stock tcmalloc, Rayne won't hook the system allocation functions like `malloc()` and `new`, instead, it overrides the global `new` and `delete` operators. This is useful to ensure that libraries that depend on their own memory management functions can continue to use them, however, this also means that a pointer allocated opaque within a different library should not be managed by Raynes memory management functions. However, well engineered usually provide ways of dealing with their memory without any hassle, so that shouldn't be too much of a problem.

Usually you don't need to allocate memory using one of these functions, just make sure that the `Rayne.h` umbrella header is included before any other header that might interfere with memory management and use the global `new` and `delete` operators.

Functions
=========

.. function:: void *AllocateAligned(size_t size, size_t alignment)

	Allocates an aligned block of memory of size `size` with alignment `alignment`.

.. function:: void *AllocateSIMD(size_t size)

	Allocates a block of memory of size `size` that satisfies SIMD requirements of the current architecture.

.. function:: void FreeAligned(void *pointer)

	Frees an aligned block of memory allocated by `AllocateAligned`

.. function:: void FreeSIMD(void *pointer)

	Frees a block of memory that was allocated by `AllocateSIMD`

.. function:: void *Allocate(size_t size)

	Allocates a new block of memory. This method is the equivalent of `new` in C++

.. function:: void *AllocateArray(size_t size)

	Allocates a new block of memory for array usage. This method is the equivalent of `new []` in C++

.. function:: void *Allocate(size_t size, const std::nothrow_t& n) noexcept

	Allocates a new block of memory. This method is the equivalent of `new` with the noexcept qualifier in C++

.. function:: void *AllocateArray(size_t size, const std::nothrow_t& n) noexcept

	Allocates a new block of memory for array usage. This method is the equivalent of `new []` with the noexcept qualifier in C++

.. function:: void Free(void *ptr) noexcept

	Frees a block of memory that was obtained by `Allocate`

.. function:: void FreeArray(void *ptr) noexcept

	Frees a block of memory that was obtained by `AllocateArray`

.. function:: void Free(void *ptr, const std::nothrow_t& n) noexcept

	Frees a block of memory that was obtained by `Allocate`

.. function:: void FreeArray(void *ptr, const std::nothrow_t& n) noexcept
	
	Frees a block of memory that was obtained by `AllocateArray`
	
