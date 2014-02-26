.. _rnthread.rst:

**********************
Thread class reference
**********************

.. namespace:: RN
.. class:: Thread

+-------------------+---------------------+
| **Inherits from** | :cpp:class:`Object` |
+-------------------+---------------------+
| **Availability**  | Rayne 1.0           |
+-------------------+---------------------+
| **Declared in**   | RNThread.h          |
+-------------------+---------------------+

Overview
========

The thread class provides a high level abstraction over a kernel thread. It provides additional information about the state of the thread, as well as synchronization methods and a high level, shared, thread local storage.

Tasks
=====

Creating and accessing threads
------------------------------

* :cpp:func:`Thread(F &&func, bool detach = true) <Thread::Thread>`
* :cpp:func:`Thread(Function &&func, bool detach = true) <Thread::Thread>`
* :cpp:func:`GetCurrentThread() <Thread::GetCurrentThread>`
* :cpp:func:`GetMainThread() <Thread::GetMainThread>`

Execution and state
-------------------

* :cpp:func:`Detach() <Thread::Detach>`
* :cpp:func:`WaitForExit() <Thread::WaitForExit>`
* :cpp:func:`OnThread() const <Thread::OnThread>`
* :cpp:func:`Cancel() <Thread::Cancel>`
* :cpp:func:`IsCancelled() const <Thread::IsCancelled>`
* :cpp:func:`IsRunning() const <Thread::IsRunning>`

Thread properties
-----------------

* :cpp:func:`SetName(const std::string &name) <Thread::SetName>`
* :cpp:func:`GetName() <Thread::GetName>`
* :cpp:func:`SetObjectForKey(Object *object, Object *key) <Thread::SetObjectForKey>`
* :cpp:func:`GetObjectForKey(Object *key) <Thread::GetObjectForKey>`
* :cpp:func:`RemoveObjectForKey(Object *key) <Thread::RemoveObjectForKey>`



Class Methods
=============

.. class:: Thread

	.. function:: Thread *GetCurrentThread()

		Returns the currently executing thread.

		.. note:: This function only works on threads that were created using the Thread class and the main thread, it doesn't work on threads created via `std::thread`, `pthread` or similar means.

	.. function:: Thread *GetMainThread()

		Returns a pointer to the main thread

		.. note:: This function only works after the :cpp:class:`Kernel` is initialized completely


Instance Methods
================

.. class:: Thread
	
	.. function:: Thread(F &&func, bool detach = true)

		Creates a new thread with the given functional as function. The functional can either be a lambda, a bound function, a function pointer or similar, as long as it provides the function call operator. If detach is true, the thread will automatically detach and run.

	.. function:: Thread(Function &&func, bool detach = true)

		Creates a new thread with the given function object. If detach is true, the thread will automatically detach and run.

	.. function:: void Detach()

		Detaches the thread. A thread must be detached before it can run.

		.. note:: If the thread is already detached, this will throw an inconsistency exception.

	.. function:: void WaitForExit()

		Blocks the calling thread until the threads finishes execution. This is a no-op in case it's called on the calling thread.

	.. function:: bool OnThread() const

		Returns true if called on the calling thread, otherwise false.

	.. function:: void Cancel()

		Marks the receiver as cancelled. Cancellation is up to the actual implementation of the thread to implement, however, it's encouraged that cancellable threads check this property periodically and gracefully exit execution.

	.. function:: bool IsCancelled() const

		Returns true if the thread is marked as cancelled

	.. function:: bool IsRunning() const

		Returns true if the thread is currently running. A detached thread is not automatically running until it receives its first time slice by the OS and actually started executing instructions.

	.. function:: void SetName(const std::string &name)

		Sets the name of the thread. The name appears in the debugger, crash logs and the IDE and is useful for debugging purposes. By default, threads get `RN::Thread` followed by a unique number as name.

		.. note:: Due to limitations in the underlying implementation of the different targets Rayne runs on, you can only set names for threads that either aren't detached yet, or for the calling thread itself.

	.. function:: std::string GetName()

		Returns the name of the receiver.

	.. function:: void SetObjectForKey(Object *object, Object *key)

		Associates the given key with the given object in the internal thread dictionary. This allows using the thread as high level thread local storage, which can additionally also be accessed by other threads. Another use case is giving additional data to the thread before detaching it.

		.. note:: The key must be copyable.

	.. function:: T *GetObjectForKey(Object *key)

		Returns the object associated with the given key, or nullptr.

	.. function:: void RemoveObjectForKey(Object *key)

		Removes the object associated with the given key.
