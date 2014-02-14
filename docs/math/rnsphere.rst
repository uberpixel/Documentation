.. _rnsphere.rst:

***********************
Sphere class reference
***********************

.. namespace:: RN
.. class:: Sphere

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNSphere.h                           |
+---------------------+--------------------------------------+

Overview
========

The Sphere class provides an implementation for a sphere with an offset. It is mostly meant to be used for bounding spheres and allows the sphere to be aligned with a scene nodes position while still being a close fit by using an additional offset which then has to be rotated with the scene node.
Bounding spheres are automatically created and updated for each scene node.

Tasks
=====

Construction
------------

* :cpp:func:`Sphere() <Sphere::Sphere>`
* :cpp:func:`Sphere(const Vector3& offset, float radius) <Sphere::Sphere>`
* :cpp:func:`Sphere(const AABB& aabb) <Sphere::Sphere>`
  
Binary operators
----------------

* :cpp:func:`operator* (const Vector3& other) const <Sphere::operator*>`
* :cpp:func:`operator*= (const Vector3& other) <Sphere::operator*=>`

Mutation
--------

* :cpp:func:`SetRotation(const Quaternion& rotation) <Sphere::SetRotation>`

Checks
------

* :cpp:func:`CastRay(const Vector3 &position, const Vector3 &direction) const <Sphere::CastRay>`
* :cpp:func:`IntersectsRay(const Vector3 &position, const Vector3 &direction) const <Sphere::IntersectsRay>`

  
Instance Methods
================

.. class:: Sphere 

	.. function:: Sphere()

		Initializes all components of position, offset and radius with 0.0f.

	.. function:: Sphere(const Vector3& offset, float radius)

		Initializes the position with 0 and offset and radius with the given values.

	.. function:: Sphere(const AABB& aabb)

		Initializes the sphere to include the given AABB.

	.. function:: Sphere operator* (const Vector3& other) const

		Returns a new sphere with the radius and offset scaled with the vector. The radius is scaled with the biggest value of the vector.

	.. function:: Sphere& operator*= (const Vector3& other)

		Scales the spheres offset and radius with the vector, using only the biggest value for scaling the radius

	.. function:: void SetRotation(const Quaternion& rotation)

		Rotates the spheres offset.

	.. function:: Hit CastRay(const Vector3 &position, const Vector3 &direction) const

		Returns hit information if the given ray hits the sphere at some point.

	.. function:: bool IntersectsRay(const Vector3 &position, const Vector3 &direction) const

		Returns true if the given ray hits the sphere at some point.

Members
=======

.. class:: Sphere

	.. member:: Vector3 position

		The position of the sphere in world space.

	.. member:: Vector3 offset

		The current offset of the sphere.

	.. member:: float radius

		The spheres radius.

