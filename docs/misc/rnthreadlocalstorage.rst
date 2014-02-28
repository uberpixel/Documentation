.. _rnthreadlocalstorage.rst:

************************************
thread_local_storage class reference
************************************

.. namespace:: RN
.. namespace:: stl
.. class:: thread_local_storage 

+------------------+------------------------+
| **Availability** |       Rayne 1.0        |
+------------------+------------------------+
| **Declared in**  | RNThreadLocalStorage.h |
+------------------+------------------------+
| **Namespace**    | stl                    |
+------------------+------------------------+

Overview
========

The thread_local_storage class implements a "smart", templated thread local storage that also gives access to all stored values and the ability to clean all of them at once. Due to its nature, it introduces a bit more overhead than a classical thread local storage, which should be preferred is storing thread local data is all that is required.

The full declaration of the method is:

.. code:: cpp

	template<class T>
	class thread_local_storage

Instance Methods
================

.. class:: thread_local_storage

	.. function:: T &get()

		Returns the object local to the calling thread

	.. function:: void clear()

		Clears all objects for all threads. This effectively resets the thread local storage.

	.. function:: void clear_local()

		Clears the object local to the calling thread

	.. function:: std::vector<T> values() const

		Returns all objects that the thread local storage is currently handling

	.. function:: T &operator *()

		Accesses the object local to the calling thread

	.. function:: const T &operator *()

		Accesses the object local to the calling thread

	.. function:: T *operator ->()

		Accesses the object local to the calling thread

	.. function:: const T *operator ->() const

		Accesses the object local to the calling thread

