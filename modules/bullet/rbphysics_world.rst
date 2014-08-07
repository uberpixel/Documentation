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
* :cpp:func:`~PhysicsWorld() override <PhysicsWorld::~PhysicsWorld override>`

Getters and Setters
-------------------

* :cpp:func:`SetGravity() <PhysicsWorld::SetGravity>`
* :cpp:func:`GetBulletDynamicsWorld() <PhysicsWorld::GetBulletDynamicsWorld>`

Actions
-------

* :cpp:func:`StepWorld() override <PhysicsWorld::StepWorld override>`
* :cpp:func:`InsertCollisionObject() <PhysicsWorld::InsertCollisionObject>`
* :cpp:func:`RemoveCollisionObject() <PhysicsWorld::RemoveCollisionObject>`
* :cpp:func:`CastRay() <PhysicsWorld::CastRay>`

Instance Methods
================

TBA
