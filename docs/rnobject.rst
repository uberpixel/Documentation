.. _rnobject.rst:

**********************
Object class reference
**********************

.. namespace:: RN
.. class:: Object 

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNObject.h                           |
+---------------------+--------------------------------------+
| **Companion guide** | :ref:`naming.rst`                    |
+---------------------+--------------------------------------+

Overview
========

Object implements the root class for most other high level classes in Rayne. It provides
a reference counting environment, and together with the class catalogue means for runtime
type introspection.

Each Object also maintains a recursive spin lock, which can be locked and unlocked via the :cpp:func:`Lock <Object::Lock>` and :cpp:func:`Unlock <Object::Unlock>` methods.

Memory management
-----------------

Object and its concrete subclasses implement a reference counting environment, that is, they maintain an internal counter
for the references that are held to the object itself. If the counter drops to zero, the object is automatically deleted.
Objects start with a reference count of 1 upon creation, and you can add a reference by calling :cpp:func:`Retain <Object::Retain>` on the object (incrementing the reference counter by 1) and relinquish a reference by calling :cpp:func:`Release <Object::Release>`.

The reference counting brings numerous advantages, however, it also means that you shouldn't create objects on the stack or call delete directly on them (with the only exception being the :cpp:class:`Array` class).

Subclassing notes
-----------------

To play nicely with the Objects runtime type introspection system, you are advised to add appropriate invocation the :c:macro:`RNDefineMeta <RNDefineMeta>` and :c:macro:`RNDeclareMeta <RNDeclareMeta>` macros.

Tasks
=====

Initializing a class
--------------------
* :cpp:func:`InitialWakeUp() static <Object::InitialWakeUp>`
  
Construction/Destruction
------------------------

* :cpp:func:`Object() <Object::Object>`
* :cpp:func:`virtual ~Object() <Object::~Object>`
* :cpp:func:`virtual CleanUp() <Object::CleanUp>`
* :cpp:func:`Copy() const <Object::Copy>`
  
Memory management
-----------------

* :cpp:func:`Retain() <Object::Retain>`
* :cpp:func:`Release() <Object::Release>`
* :cpp:func:`Autorelease() <Object::Autorelease>`

Identifying objects
-------------------

* :cpp:func:`Class() const <Object::Class const>`
* :cpp:func:`MetaClass() static <Object::MetaClass>`
* :cpp:func:`IsKindOfClass() const <Object::IsKindOfClass const>`
* :cpp:func:`IsMemeberOfClass() const <Object::IsMemberOfClass const>`
* :cpp:func:`Downcast() <Object::Downcast>`

Comparing objects
-----------------

* :cpp:func:`virtual IsEqual() const <Object::IsEqual const>`
* :cpp:func:`virtual GetHash() const <Object::GetHash const>`
  
Serialization
-------------

* :cpp:func:`virtual Serialize() <Object::Serialize>`

Associating objects
-------------------

* :cpp:func:`SetAssociatedObject() <Object::SetAssociatedObject>`
* :cpp:func:`RemoveAssociatedOject() <Object::RemoveAssociatedOject>`
* :cpp:func:`GetAssociatedObject() <Object::GetAssociatedObject>`
  
Locking and synchronization
---------------------------

* :cpp:func:`Lock() <Object::Lock>`
* :cpp:func:`Unlock() <Object::Unlock>`

Class Methods
=============

.. class:: Object 

	.. function:: static MetaClassBase *MetaClass()

		Returns the :code:`MetaClassBase` of the receiver.

	.. function:: static void InitialWakeUp(MetaClassBase *meta)

		Automatically invoked when the class is added to the class catalogue. Can be used
		to defer initialization to the runtime when the engine is already bootstrapped.

		When overriding this method, make sure to check that the passed :code:`meta` variable is
		actually the expected MetaClassBase, since this method may be invoked multiple times through
		subclasses.

	.. admonition:: Example

		.. code:: cpp

			void MyClass::InitialWakeUp(MetaClassBase *meta)
			{
			    if(meta == MyClass::MetaClass())
			    {
			        // Code here
			    }
			}

Instance Methods
================

.. class:: Object 

	.. function:: Object()

		The designated constructor for object. Sets up internal locks and other state

	.. function:: ~Object()

		Destructor. Automatically cleans up the objects associated with the receiver, and
		if the debug engine build is used, does some extra sanity checks.

	.. function:: void CleanUp()

		This method is automatically called when the reference count of the receiver drops to zero,
		but before it's deleted. This method is :emphasis:`vitally` important in the Rayne multithreaded
		environment and should be the preferred point for cleaning up the instance and synchronizing because
		it's invoked before the vtable of the receiver is touched, and thus avoids races to the vtable when
		doing synchronization operations (eg. waiting for a task to finish that was started via a virtual method).

	.. function:: Object *Copy() const

		Attempts to create a copy of the receiver by calling the copy constructor through the runtime introspection
		system.

		:raises: :code:`InternalInconsistencyException` when the receiver doesn't support the :cpp:class:`MetaClassTraitCopyable` trait.

	.. function:: MetaClassBase *Class() const

		Returns the :code:`MetaClassBase` of the receiver.

	.. function:: bool IsKindOfClass(MetaClassBase *other) const

		Returns true if the receiver inherits from the class abstracted by :code:`other`, that is,
		if you pass :code:`Object::MetaClass`, the receiver will return true if it inherits from :cpp:class:`Object`,
		or one of its subclasses (or one of their subclasses respectively).

		.. seealso:: :cpp:func:`Object::IsMemberOfClass`

	.. function:: bool IsMemberOfClass(MetaClassBase *other) const

		Returns true if the receiver directly inherits from the class abstracted by :code:`other`.

		.. seealso:: :cpp:func:`Object::IsKindOfClass`

	.. function:: Object *Retain()

		Increments the retain count of the receiver by 1

		:return: Pointer to the instance, allowing method chaining

	.. function:: Object *Release()

		Decrements the retain count of the receiver by 1. If the retain count becomes zero,
		the receiver is deleted and its destructor is called.

		:return: Pointer to the instance, or :code:`nullptr` if the instance was deallocated.

	.. function:: Object *Autorelease()

		Adds the receiver to the current threads autorelease pool, marking it to be released in the future.
		The method should be used for return values when the callee doesn't explicitly delegates the ownership of the object to the caller.

		:return: Pointer to the instance, allowing method chaining

	.. function:: bool IsEqual(Object *other) const
		
		Returns true if :code:`other` is equal to the receiver. The default implementation simply checks for pointer equality,
		subclasses may provide a custom and more sophisticated check.

		:param other: The object to check for equality with the receiver
		:return: true if the objects are equal, otherwise false

		.. note:: When overriding IsEqual(), GetHash() must also be overridden
		.. note:: This method is not inherently thread safe
		.. seealso:: :cpp:func:`Object::Hash`

	.. function:: machine_hash GetHash() const

		Returns the hash for the receiver. The default implementation returns the hashed value of the pointer of the instance,
		subclasses may provide a custom hashing function (eg. the :cpp:class:`String` class returns the hash of the string value).

		As long as the receiver isn't mutated, the returned hash is guaranteed to stay the same, and equal objects return the same
		hash (that is, if :cpp:func:`IsEqual` returns true, the hash returned by this function is the same for both objects). This
		behaviour must be adopted when overriding this function in subclasses!

		:return: The hash value for the object.

		.. note:: When overriding Hash(), IsEqual() must also be overridden
		.. note:: This method is not inherently thread safe
		.. seealso:: :cpp:func:`Object::IsEqual`

	.. function:: T *Downcast()
		
		Attempts to downcast the receiver to the given type T, where T must inherit of Object

		:returns: The same instance, but downcasted to T. The return value is always valid.
		:raises: DowncastException if no conversion to T is possible
		:raises: Static assertion if T doesn't inherit from Object

		.. admonition:: Example

			.. code:: cpp

				Object *foo = ...;
				String *bar = foo->Downcast<String>();

	.. function:: void SetAssociatedObject(const void *key, Object *value, MemoryPolicy policy)

		Associates the given object with the given key using the given memory policy. An association works similar to an instance variable,
		but isn't part of the class layout and thus arbitrary objects can be associated with other objects without changing their class layouts
		(which is useful when subclassing isn't ideal and altering the class isn't possible). Note though that associations are in no way
		a replacement for instance variables, since they come with additional overhead when retrieving and storing associations!

		.. seealso:: 
			| :cpp:func:`RemoveAssociatedOject` 
			| :cpp:func:`GetAssociatedObject` 
			| :cpp:type:`MemoryPolicy`

	.. function:: void RemoveAssociatedOject(const void *key)

		Removes the object associated with the given key from the receiver. If the key was associated with either :cpp:type:`MemoryPolicy::Retain` or :cpp:type:`MemoryPolicy::Copy`,
		the associated object will automatically receive a :cpp:func:`Release` method.

		.. seealso:: 
			| :cpp:func:`SetAssociatedObject` 
			| :cpp:func:`GetAssociatedObject` 

	.. function:: Object *GetAssociatedObject(const void *key)

		Returns the object associated with the given key, or :code:`nullptr` if no object is associated with the key.

		.. seealso:: 
			| :cpp:func:`SetAssociatedObject` 
			| :cpp:func:`RemoveAssociatedOject` 


	.. function:: void Lock()

		Locks the receivers internal recursive spin lock.
		Keep in mind that this is just a recursive spin lock and should only be held for a small amount of time, heavy
		synchronization should be done using a full blown mutex

		.. seealso:: :cpp:func:`Unlock`

	.. function:: void Unlock()

		Unlocks the receivers internal recursive spin lock.

		.. seealso:: :cpp:func:`Lock`
		
Constants
=========

.. class:: Object 

	.. type:: MemoryPolicy
		
		* :code:`Assign` A simple assignment, there is no memory management done
		* :code:`Retain` Retain policy which retains the receiver
		* :code:`Copy` Copy policy which creates a shallow copy

Macros
======

.. c:macro:: RNDeclareMeta(cls, super)

	Adds required prototypes for the runtime type system to the given class. Must be added within the class definition.

	.. admonition:: Example

		.. code:: cpp

			class MyClass : public Object
			{
			public:
				// ...

			private:
				// ...

				RNDefineMeta(MyClass, Object)
			};

.. c:macro:: RNDefineMeta(cls)

	Adds required implementations for the runtime type system to the given class. MUST be added within a .cpp file due to the way linking works.

