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
* :cpp:func:`~RigidBody() override <RigidBody::~RigidBody>`
* :cpp:func:`WithShape() static <RigidBody::WithShape>`
* :cpp:func:`WithShapeAndInertia() static <RigidBody::WithShapeAndInertia>`

Getters and Setters
-------------------

* :cpp:func:`GetLinearVelocity() const <RigidBody::GetLinearVelocity const>`
* :cpp:func:`SetLinearVelocity() <RigidBody::SetLinearVelocity>`
* :cpp:func:`GetAngularVelocity() const <RigidBody::GetAngularVelocity const>`
* :cpp:func:`SetAngularVelocity() <RigidBody::SetAngularVelocity>`
* :cpp:func:`GetCenterOfMass() const <RigidBody::GetCenterOfMass const>`
* :cpp:func:`GetCenterOfMassTransform() const <RigidBody::GetCenterOfMassTransform const>`
* :cpp:func:`SetMass() <RigidBody::SetMass>`
* :cpp:func:`SetCCDMotionThreshhold() <RigidBody::SetCCDMotionThreshold>`
* :cpp:func:`SetCCDSweptSphereRadius() <RigidBody::SetCCDSweptSphereRadius>`
* :cpp:func:`SetGravity() <RigidBody::SetGravity>`
* :cpp:func:`SetDamping() <RigidBody::SetDamping>`
* :cpp:func:`GetBulletCollisionObject() override <RigidBody::GetBulletCollisionObject>`
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

.. class:: RigidBody

	.. function:: static RigidBody *WithShape(Shape *shape, float mass)

		Constructor using a static method; creates a new body with a shape and mass.

	.. function:: static RigidBody *WithShapeAndInertia(Shape *shape, float mass, const Vector3 &inertia)

		Constructor using a static method; creates a new body with a shape, mass and inertia.

Instance Methods
================

.. class:: RigidBody

	.. function:: RigidBody(Shape *shape, float mass)

		Default constructor; creates a new body with a shape and mass.

	.. function:: RigidBody(Shape *shape, float mass, const Vector3 &inertia)

		Default constructor; creates a new body with a shape, mass and inertia.

	.. function:: ~RigidBody() override

		Default destructor.

	.. function:: void SetMass(float mass)

		Set the mass of the body.

	.. function:: void SetMass(float mass, const Vector3 &inertia)

		Set the mass and inertia of the body.

	.. function:: void SetLinearVelocity(const Vector3 &velocity)

		Set the current speed of the object.

	.. function:: void SetAngularVelocity(const Vector3 &velocity)

		Set the current rotational speed of the object.

	.. function:: void SetCCDMotionThreshold(float threshold)

		Set the motion threshold for continuous collision detection. This is the amount of distance the engine waits before testing a sphere defined with :cpp:func:`SetCDDSweptSphereRadius <SetCCDSweptSphereRadius>` to prevent a fast-moving object from going through something else.

	.. function:: void SetCCDSweptSphereRadius(float radius)

		Set the sphere size for continuous collision detection. This is used for testing a sphere instead of testing with the entire shape for collisions between frames because it is far more efficient.

	.. function:: void SetGravity(const Vector3 &gravity)

		Set the gravity of the object

	.. function:: void SetDamping(float linear, float angular)

		Set the damping for the object. Damping is the reduction of the amplitude of vibrations.

	.. function:: void ApplyForce(const Vector3 &force)

		Push an object in the direction of the vector specified.

	.. function:: void ApplyForce(const Vector3 &force, const Vector3 &origin)

		Push an object in the direction of the vector specified about the origin.

	.. function:: void ClearForces()

		Reset the forces on an object.

	.. function:: void ApplyTorque(const Vector3 &torque)

		Apply a force to the object about the vector provided.

	.. function:: void ApplyTorqueImpulse(const Vector3 &torque)

		Apply an impulse to the object about the vector provided.

	.. function:: void ApplyImpulse(const Vector3 &impulse)

		Shove an object in the direction of the vector specified.

	.. function:: void ApplyImpulse(const Vector3 &impulse, const Vector3 &origin)

		Shove an object in the direction of the vector specified about the origin.

	.. function:: Vector3 GetLinearVelocity() const

		Get the amount of force on the object.

	.. function:: Vector3 GetAngularVelocity() const

		Get the amount of angular force on the object.

	.. function:: Vector3 GetCenterOfMass() const

		The position representing the center of mass for the object.

	.. function:: Matrix GetCenterOfMassTransform() const

		Get transform data for the object about the center of mass.

	.. function:: btCollisionObject *GetBulletCollisionObject()

		Get a raw bullet collision object for advanced usage.

	.. function:: btRigidBody *GetBulletRigidBody()

		Get a raw bullet physics object for advanced usage.
