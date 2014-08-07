.. _rbcollision_object.rst

*******************************
CollisionObject class reference
*******************************

.. namespace:: RN
.. namespace:: bullet
.. class:: CollisionObject

+-------------------+----------------------------------+
| **Inherits from** | :cpp:class:`SceneNodeAttachment` |
+-------------------+----------------------------------+
| **Availability**  | rayne-bullet                     |
+-------------------+----------------------------------+
| **Declared in**   | RBCollisionObject.h              |
+-------------------+----------------------------------+
| **Namespace**     | bullet                           |
+-------------------+----------------------------------+

Overview
========

TBA

Tasks
=====

Construction and Destruction
----------------------------

* :cpp:func:`CollisionObject() <CollisionObject::CollisionObject>`
* :cpp:func:`~CollisionObject() override <CollisionObject::~CollisionObject>`

Getters and Setters
-------------------

* :cpp:func:`GetCollisionFilter() const <CollisionObject::GetCollisionFilter const>`
* :cpp:func:`SetCollisionFilter() <CollisionObject::SetCollisionFilter>`
* :cpp:func:`GetCollisionFilterMask() const <CollisionObject::GetCollisionFilterMask const>`
* :cpp:func:`SetCollisionFilterMask() <CollisionObject::SetCollisionFilterMask>`
* :cpp:func:`GetMaterial() const <CollisionObject::GetMaterial const>`
* :cpp:func:`SetMaterial() <CollisionObject::SetMaterial>`
* :cpp:func:`virtual GetBulletCollisionObject() <CollisionObject::GetBulletCollisionObject>`
* :cpp:func:`SetContactCallback() <CollisionObject::SetContactCallback>`

Instance Methods
================

.. class:: CollisionObject

	.. function:: CollisionObject()

		Default constructor.

	.. function:: ~CollisionObject() override

		Default destructor.

	.. function:: void SetCollisionFilter(short int filter)

		Set the filter for determining what this can collide with.

	.. function:: void SetCollisionFilterMask(short int mask)

		Set the filter mask for determining what this can collide with.

	.. function:: void SetMaterial(PhysicsMaterial *material)

		Set the :cpp:class:`PhysicsMaterial <PhysicsMaterial>` for this object.

	.. function:: void SetContactCallback(std::function<void(CollisionObject *)> &&callback)

		Determine what happens upon collision with another.

	.. function:: short int GetCollisionFilter() const

		Get the filter for determining what this can collide with.

	.. function:: short int GetCollisionFilterMask() const

		Get the filter mask for determining what this can collide with.

	.. function:: PhysicsMaterial *GetMaterial() const

		Get the :cpp:class:`PhysicsMaterial <PhysicsMaterial>` for this object.

	.. function:: btCollisionObject *GetBulletCollisionObject()

		Get the raw bullet object for advanced uses.
