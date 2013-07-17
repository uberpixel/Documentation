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

* :cpp:func:`Class() <Object::Class const>`
* :cpp:func:`MetaClass() <Object::MetaClass>`
* :cpp:func:`IsKindOfClass() <Object::IsKindOfClass const>`
* :cpp:func:`IsMemeberOfClass() <Object::IsMemberOfClass const>`
* :cpp:func:`Downcast() <Object::Downcast const>`

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

.. function:: static MetaClassBase *Object::MetaClass()

Instance Methods
================

.. function:: MetaClassBase *Object::Class() const

.. function:: bool Object::IsKindOfClass(MetaClassBase *other) const

.. function:: bool Object::IsMemberOfClass(MetaClassBase *other) const

.. function:: Object *Object::Retain()

.. function:: Object *Object::Release()

.. function:: Object *Object::Autorelease()

.. function:: bool Object::IsEqual(Object *other) const
	
	Returns true if other is equal to the receiver. The default implementation simply checks for pointer equality,
	subclasses may provide a custom and more sophisticated check.

	.. note:: When overriding IsEqual(), Hash() must also be overridden, and equal objects must return the same hash
	.. seealso:: :cpp:func:`Object::Hash`

	:param other: The object to check for equality with the receiver
	:param foo: Barfoo
	:return: true if the objects are equal, otherwise false

.. function:: machine_hash Object::Hash() const

	Returns a hash for the receiver. The default implementation returns the hashed value of the pointer of the instance,
	subclasses may provide a custom hashing function (eg. the :cpp:class:`String` class returns the hash of the string value).

.. function:: T *Object::Downcast() const
	
	Attempts to downcast the receiver to the given type T.

	*Example:*

	.. code:: cpp

		Object *foo = ...;
		String *bar = foo->Downcast<String>();


	:returns: The same instance, but downcasted to T. The return value is always valid.
	:raises: DowncastException if no conversion to T is possible
	:raises: Static assertion if T doesn't inherit from Object (or one of its subclasses)

.. function:: void Object::SetAssociatedObject(const void *key, Object *value, MemoryPolicy policy)

.. function:: void Object::RemoveAssociatedOject(const void *key)

.. function:: Object *Object::AssociatedObject(const void *key)
	
Constants
=========

.. type:: Object::MemoryPolicy
	
	* :code:`Assign`
	* :code:`Retain`
	* :code:`Copy`
