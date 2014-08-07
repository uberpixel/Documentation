.. _rbrigid_body.rst

*******************************
RigidBody class reference
*******************************

.. namespace:: RN
.. namespace:: bullet
.. class:: RigidBody

+-------------------+------------------------------+
| **Inherits from** | :cpp:class:`CollisionObject` |
+-------------------+------------------------------+
| **Availability**  | rayne-bullet                 |
+-------------------+------------------------------+
| **Declared in**   | RBRigidBody.h                |
+-------------------+------------------------------+
| **Namespace**     | bullet                       |
+-------------------+------------------------------+

Overview
========

TBA

Tasks
=====

Construction and Destruction
----------------------------

* :cpp:func:`RigidBody() <RigidBody::RigidBody>`
* :cpp:func:`~RigidBody() override <RigidBody::~RigidBody override>`
* :cpp:func:`WithShape() static <RigidBody::WithShape static>`
* :cpp:func:`WithShapeAndInertia() static <RigidBody::WithShapeAndInertia static>`

Getters and Setters
-------------------

* :cpp:func:`GetLinearVelocity() const <RigidBody::GetLinearVelocity const>`
* :cpp:func:`SetLinearVelocity() <RigidBody::SetLinearVelocity>`
* :cpp:func:`GetAngularVelocity() const <RigidBody::GetAngularVelocity const>`
* :cpp:func:`SetAngularVelocity() <RigidBody::SetAngularVelocity>`
* :cpp:func:`GetCenterOfMass() const <RigidBody::GetCenterOfMass const>`
* :cpp:func:`GetCenterOfTransform() const <RigidBody::GetCenterOfTransform const>`
* :cpp:func:`SetMass() <RigidBody::SetMass>`
* :cpp:func:`SetCCDMotionThreshhold() <RigidBody::SetCCDMotionThreshold>`
* :cpp:func:`SetCCDSweptSphereRadius() <RigidBody::SetCCDSweptSphereRadius>`
* :cpp:func:`SetGravity() <RigidBody::SetGravity>`
* :cpp:func:`SetDamping() <RigidBody::SetDamping>`
* :cpp:func:`GetBulletCollisionObject() override <RigidBody::GetBulletCollisionObject override>`
* :cpp:func:`GetBulletRigidBody() <RigidBody::GetBulletRigidBody>`

Actions
-------

* :cpp:func:`ApplyForce() <RigidBody::ApplyForce>`
* :cpp:func:`ClearForces() <RigidBody::ClearForces>`
* :cpp:func:`ApplyImpulse() <RigidBody::ApplyImpulse>`
* :cpp:func:`ApplyTorque() <RigidBody::ApplyTorque>`
* :cpp:func:`ApplyTorqueImpulse() <RigidBody::ApplyTorqueImpulse>`

Class Methods
=============

TBA

Instance Methods
================

TBA
