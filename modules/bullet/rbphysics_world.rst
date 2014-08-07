.. _rbphysics_world.rst

****************************
PhysicsWorld class reference
****************************

.. namespace:: RN
.. namespace:: bullet
.. class:: PhysicsWorld

+-------------------+-----------------------------------------------------------------------------------------+
| **Inherits from** | :cpp:class:`WorldAttachment`                                                            |
+-------------------+-----------------------------------------------------------------------------------------+
|                   | :cpp:class:`INonConstructingSingleton\<PhysicsWorld\> <INonConstructingSingleton\<T\>>` |
+-------------------+-----------------------------------------------------------------------------------------+
| **Availability**  | rayne-bullet                                                                            |
+-------------------+-----------------------------------------------------------------------------------------+
| **Declared in**   | RBPhysicsWorld.h                                                                        |
+-------------------+-----------------------------------------------------------------------------------------+
| **Namespace**     | bullet                                                                                  |
+-------------------+-----------------------------------------------------------------------------------------+

Overview
========

TBA

Tasks
=====

Construction and Destruction
----------------------------

* :cpp:func:`PhysicsWorld() <PhysicsWorld::PhysicsWorld>`
* :cpp:func:`~PhysicsWorld() override <PhysicsWorld::~PhysicsWorld>`

Getters and Setters
-------------------

* :cpp:func:`SetGravity() <PhysicsWorld::SetGravity>`
* :cpp:func:`GetBulletDynamicsWorld() <PhysicsWorld::GetBulletDynamicsWorld>`

Actions
-------

* :cpp:func:`StepWorld() override <PhysicsWorld::StepWorld>`
* :cpp:func:`InsertCollisionObject() <PhysicsWorld::InsertCollisionObject>`
* :cpp:func:`RemoveCollisionObject() <PhysicsWorld::RemoveCollisionObject>`
* :cpp:func:`CastRay() <PhysicsWorld::CastRay>`

Instance Methods
================

.. class:: PhysicsWorld

	.. function:: PhysicsWorld(const Vector3 &gravity=Vector3(0.0f,-9.81f,0.0f))
	
		Default constructor. Takes an initial gravity for the world.

	.. function:: ~PhysicsWorld() override

		Default destructor.

	.. function:: void SetGravity(const Vector3 &gravity)

		Change the gravity for the world.

	.. function:: void StepWorld(float delta) override

		Update the world as the time specified has passed.

	.. function:: Hit CastRay(const Vector3 &from, const Vector3 &to)

		Check collisions along a line segment.

	.. function:: void InsertCollisionObject(CollisionObject *attachment)
	
		Add a new object to the simulation.

	.. function:: void RemoveCollisionObject(CollisionObject *attachment)

		Remove an object from the simulation.

	.. function:: btDynamicsWorld *GetBulletDynamicsWorld()

		Get the raw bullet object for advanced usage.
