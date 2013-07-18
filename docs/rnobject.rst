.. _rnobject.rst:

***************************
Object class reference
***************************

.. namespace:: RN
.. class:: Object 

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNObject.h                           |
+---------------------+--------------------------------------+
| **Companion guide** | :ref:`getting_started.rst`           |
+---------------------+--------------------------------------+
| **Sample code**     | :ref:`Example <getting_started.rst>` |
+---------------------+--------------------------------------+

Overview
========

Object implements the root class for most high level classes in Rayne.

Tasks
=====

Identifying objects
-------------------

* :cpp:func:`Class() const <Object::Class const>`
* :cpp:func:`MetaClass() <Object::MetaClass>`
* :cpp:func:`IsKindOfClass() const <Object::IsKindOfClass const>`
* :cpp:func:`IsMemeberOfClass() const <Object::IsMemberOfClass const>`
* :cpp:func:`Downcast() <Object::Downcast>`

Comparing objects
-----------------

* :cpp:func:`IsEqual() <Object::IsEqual>`
* :cpp:func:`Hash() <Object::Hash>`

Memory management
-----------------

* :cpp:func:`Retain() <Object::Retain>`
* :cpp:func:`Release() <Object::Release>`
* :cpp:func:`Autorelease() <Object::Autorelease>`

Associating objects
-------------------

* :cpp:func:`SetAssociatedObject() <Object::SetAssociatedObject>`
* :cpp:func:`RemoveAssociatedOject() <Object::RemoveAssociatedOject>`
* :cpp:func:`AssociatedObject() <Object::AssociatedObject>`

Class Methods
=============

.. class:: Object 

	.. function:: static MetaClassBase *MetaClass()

Instance Methods
================

.. class:: Object 

	.. function:: MetaClassBase *Class() const

	.. function:: bool IsKindOfClass(MetaClassBase *other) const

	.. function:: bool IsMemberOfClass(MetaClassBase *other) const

	.. function:: Object *Retain()

		Increments the retain count of the receiver by 1

		:return: Pointer to the instance, allowing method chaining

		.. note:: This method is thread safe

	.. function:: Object *Release()

		Decrements the retain count of the receiver by 1. If the retain count becomes zero,
		the instance is deleted and its constructor is called.

		:return: Pointer to the instance, or nullptr if the instance was deallocated.

		.. note:: This method is thread safe

	.. function:: Object *Autorelease()

		Adds the instance to the current threads autorelease pool, marking it to be released in the future.
		The method should be used for return values when the callee doesn't explicitly delegates the ownership of the object to the caller.

		:return: Pointer to the instance, allowing method chaining

		.. note:: This method is thread safe

	.. function:: bool IsEqual(Object *other) const
		
		Returns true if other is equal to the receiver. The default implementation simply checks for pointer equality,
		subclasses may provide a custom and more sophisticated check.

		:param other: The object to check for equality with the receiver
		:return: true if the objects are equal, otherwise false

		.. note:: When overriding IsEqual(), Hash() must also be overridden, and equal objects must return the same hash
		.. seealso:: :cpp:func:`Object::Hash`

	.. function:: machine_hash Hash() const

		Returns a hash for the receiver. The default implementation returns the hashed value of the pointer of the instance,
		subclasses may provide a custom hashing function (eg. the :cpp:class:`String` class returns the hash of the string value).

		:return: The hash value for the object.

		.. note:: When overriding Hash(), IsEqual() must also be overridden, and equal objects must return the same hash
		.. seealso:: :cpp:func:`Object::IsEqual`

	.. function:: T *Downcast()
		
		Attempts to downcast the receiver to the given type T.

		:returns: The same instance, but downcasted to T. The return value is always valid.
		:raises: DowncastException if no conversion to T is possible
		:raises: Static assertion if T doesn't inherit from Object (or one of its subclasses)

		.. admonition:: Example

			.. code:: cpp

				Object *foo = ...;
				String *bar = foo->Downcast<String>();

	.. function:: void SetAssociatedObject(const void *key, Object *value, MemoryPolicy policy)

		.. note:: This method is thread safe
		.. seealso:: 
			| :cpp:func:`RemoveAssociatedOject` 
			| :cpp:func:`AssociatedObject` 
			| :cpp:type:`MemoryPolicy`

	.. function:: void RemoveAssociatedOject(const void *key)

		.. note:: This method is thread safe
		.. seealso:: 
			| :cpp:func:`SetAssociatedObject` 
			| :cpp:func:`AssociatedObject` 

	.. function:: Object *AssociatedObject(const void *key)

		.. note:: This method is thread safe
		.. seealso:: 
			| :cpp:func:`SetAssociatedObject` 
			| :cpp:func:`RemoveAssociatedOject` 
		
Constants
=========

.. class:: Object 

	.. type:: MemoryPolicy
		
		* :code:`Assign`
		* :code:`Retain`
		* :code:`Copy`
