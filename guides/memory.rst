.. _memory.rst:

***********************
Rayne memory management
***********************

Rayne provides different layers of memory management. Classes that inherit from :cpp:class:`Object` provide a reference counting memory system, which allows objects to be shared more easily between components and threads. Lower level classes like :cpp:class:`Vector3` have to be managed in the classical sense, either via `new` and `delete` or by putting them into automatic storage variables, which is the more common use case.

Automatic reference counting
============================

Rayne objects that inherit from the :cpp:class`Object` class provide a way that allows the developer to partially or completely let Raynes smart pointer system take care of the objects memory management and reference counting. This helps to reduce issues related to wrong memory management, especially dangling pointers and leaks.

There are two basic types that can be used as pointer replacement, each with a different storage clarifier: `RN::StrongRef<>` and `RN::WeakRef<>`, which provide a strong and weak reference respectively. Additionally, many built-in classes also provide typedefs, so you can write `RN::StringRef` instead of `RN::StrongRef<RN::String>` and `RN::WeakString` instead of `RN::WeakRef<RN::String`.

Strong References
-----------------

The semantic of strong references is that they hold a strong reference to the underlying object. This means that as long as the reference is in scope, the object is guaranteed to be alive. Once all smart pointers are out of scope, the object will automatically destroyed, eg the lifetime of the object is managed by the smart pointers. 

Weak References
---------------

Weak references don't hold ownership of the objects they reference to. This means that having a weak reference in scope doesn't necessarily mean the object is still alive, but the weak reference will automatically set itself to `nullptr` once the object it references is destroyed. Here is an example of how to use weak references:

.. admonition:: Example

	.. code:: cpp

		RN::WeakArray weakArray = ...; // Just assume we have a weak reference to an array that was created somewhere

		RN::ArrayRef array = weakArray;
		if(array)
		{
			array->AddObject(RNCSTR("Hello"));
			array->AddObject(RNCSTR("World"));
		}

	The weak object is accessed and stored in a strong reference, this makes sure that the object isn't accidentally destroyed in another thread and after checking if it is valid, it suddenly is destroyed (keep in mind, `nullptr` dereferencing is still undefined behaviour!). Then the object is checked if it is still valid.

Use cases for weak references are loose coupling between components, or breaking circular references where strong references point to each other.

Transferring ownership
----------------------

If you create a new object via `new`, or a method which has `Create` or `Copy` in its name, the callee will delegate ownership of the returned object to the caller. If you don't want to manually manage the memory of the object but let a smart pointer to the job, you have to transfer ownership of the object to the smart pointer, which can be done with the `RNObjectTransfer()` macro.

.. admonition:: Example

	.. code:: cpp

		RN::ArrayRef myArray = RNObjectTransfer(new RN::Array()) // This transfers the ownership of the new array to the smart pointer

		myArray = nullptr; // The smart pointer will relinquish its currently held object, ie our array
		// If we hadn't transferred the ownership to the array, all references to the array would've been lost
		// but we had still ownership to it, eg the array would leak. So always transfer ownership in these instances!

		// Similarly, let's assume myArray wouldn't point to nullptr but to an actual array:

		RN::ArrayRef myCopy = RNObjectTransfer(myArray->Copy())

Manual reference counting
=========================

Manual and automatic reference counting can be mixed. One such case might be performance concerns since smart pointer copying and weak pointer accesses can lead to a somewhat costly calls generated into the runtime. However, before you switch back to manually managing your memory, see if it is really needed, ie profile your application and see if you can benefit. And only then think about switching back to manually calling `Retain()`, `Release()` and `Autorelease()`.

Manual reference counting is described in :cpp:class:`Object`.


Working with memory in general
==============================

It is crucial that you include `RNBase.h` as the first header, as it pulls in the memory subsystem of Rayne. This allows different binaries to use the same shared memory allocator, which is provided by Rayne. This means that you can retrieve objects created by Rayne internally, and call `delete` on them yourself, which is most often not possible in C++ libraries and requires using special stubs that wrap `new` and `delete`.

Raynes uses `TCMalloc` as memory allocator, which is a high performance, thread aware memory allocator. If you have special needs on your memory, for example allocating a block of memory that has different alignment requirements than the system ABI requires (eg SIMD), you can use the `AllocateAligned()` or `AllocateSIMD()` functions found in the `RN::Memory` namespace.

.. function:: void *AllocateAligned(size_t size, size_t alignment)

	Returns a pointer to memory that is aligned to the alignment specified by alignment, or `nullptr`

.. function:: void FreeAligned(void *pointer)
	
	Frees a block of memory previously allocated via `AllocateAligned`

.. function:: void *AllocateSIMD(size_t size)
	
	Allocates a block of memory that is aligned to work with the SIMD of the current system. This means that the memory is aligned to 16 bytes boundaries for SSE and NEON.

.. function:: void FreeSIMD(void *pointer)
	
	Frees a block of memory previously allocated via `AllocateSIMD`

