.. _rbphysics_material.rst

*******************************
PhysicsMaterial class reference
*******************************

.. namespace:: RN
.. namespace:: bullet
.. class:: PhysicsMaterial

+-------------------+---------------------+
| **Inherits from** | :cpp:class:`Object` |
+-------------------+---------------------+
| **Availability**  | rayne-bullet        |
+-------------------+---------------------+
| **Declared in**   | RBPhysicsMaterial.h |
+-------------------+---------------------+
| **Namespace**     | bullet              |
+-------------------+---------------------+

Overview
========

Physics materials contain data for many of the attributes that an object might have in a physics simulation. This includes data like friction and bounciness. 

Tasks
=====

Construction
------------

* :cpp:func:`PhysicsMaterial() <PhysicsMaterial::PhysicsMaterial>`

Getters and Setters
-------------------

* :cpp:func:`GetLinearDamping() const <PhysicsMaterial::GetLinearDamping const>`
* :cpp:func:`SetLinearDamping() <PhysicsMaterial::SetLinearDamping>`
* :cpp:func:`GetAngularDamping() const <PhysicsMaterial::GetAngularDamping const>`
* :cpp:func:`SetAngularDamping() <PhysicsMaterial::SetAngularDamping>`
* :cpp:func:`GetFriction() const <PhysicsMaterial::GetFriction const>`
* :cpp:func:`SetFriction() <PhysicsMaterial::SetFriction>`
* :cpp:func:`GetRestitution() const <PhysicsMaterial::GetRestitution const>`
* :cpp:func:`SetRestitution() <PhysicsMaterial::SetRestitution>`

Instance Methods
================

.. class:: PhysicsMaterial

	.. function:: PhysicsMaterial()

		Default constructor.

	.. function:: void SetLinearDamping(float damping)
	
		Set the damping, or the rate at which vibrations decelerate.

	.. function:: void SetAngularDamping(float damping)
	
		Set the damping, or the rate at which vibrations decelerate, rotationally.

	.. function:: void SetFriction(float friction)
	
		Set the friction.

	.. function:: void SetRestitution(float restitution)

		Set the restitution, or bounciness.

	.. function:: float GetLinearDamping() const

		Get the damping, or the rate at which vibrations decelerate.
	
	.. function:: float GetAngularDamping() const

		Get the damping, or the rate at which vibrations decelerate, rotationally.
	
	.. function:: float GetFriction() const

		Get the friction.
	
	.. function:: float GetRestitution() const

		Get the restitution, or bounciness.
