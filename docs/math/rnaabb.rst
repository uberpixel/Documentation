.. _rnaabb.rst:

***********************
AABB class reference
***********************

.. namespace:: RN
.. class:: AABB

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNAABB.h                             |
+---------------------+--------------------------------------+

Overview
========

The AABB class provides an implementation for an axis aligned bounding box. Axis aligned bounding boxes are internally used for culling and automatically set and updated for scene nodes. They can also be used to get some information about a scene nodes size within the world.
Axis aligned means that it will usually change its extends when rotating a scene node, as the box itself will not rotate, but instead scale to fit the scene node.

Tasks
=====

Construction
------------

* :cpp:func:`AABB() <AABB::AABB>`
* :cpp:func:`AABB(const Vector3 &min, const Vector3 &max) <AABB::AABB>`
* :cpp:func:`AABB(const Vector3 &pos, const float radius) <AABB::AABB>`
  
Binary operators
----------------

* :cpp:func:`operator+ (const AABB& other) const <AABB::operator+>`
* :cpp:func:`operator* (const Vector3& other) const <AABB::operator*>`
* :cpp:func:`operator+= (const AABB& other) <AABB::operator+=>`
* :cpp:func:`operator*= (const Vector3& other) <AABB::operator*=>`

Mutation
--------

* :cpp:func:`SetRotation(const Quaternion& rotation) <AABB::SetRotation>`

Checks
------

* :cpp:func:`Intersects(const AABB& other) const <AABB::Intersects>`
* :cpp:func:`Contains(const Vector3 &position) const <AABB::Contains>`

  
Instance Methods
================

.. class:: AABB 

	.. function:: AABB()

		Initializes the position and extends to 0.

	.. function:: AABB(const Vector3 &min, const Vector3 &max)

		Expects min and max as positions in world scale relative to the position of the AABB and initializes minExtend and maxExtend with the minimum/maximum of the given values for each axis.

	.. function:: AABB(const Vector3 &pos, const float radius)

		Initializes the position with pos and the maxExtend with all values to radius and minExtends with all values to -radius. The resulting Bounding box will include the sphere given by pos and radius.

	.. function:: AABB& operator+ (const AABB& other) const

		Returns a new AABB with the position of the first summand but with the extends to fit both AABBs.

	.. function:: AABB operator* (const Vector3& other) const

		Returns a new AABB with the extends scaled by the vector.

	.. function:: AABB& operator+= (const AABB& other)

		Keeps the bounding boxes position but scales the extends to fit this and the other AABB.

		:return: Reference to the mutated AABB

	.. function:: AABB& operator*= (const Vector3& other)

		Scales the bounding boxes extends with the vector.

		:return: Reference to the mutated AABB

	.. function:: void SetRotation(const Quaternion& rotation)

		Rotates the bounding box. This will not change the position but scale the extends to fit the unrotated bounding box as if it was rotated.

	.. function:: bool Intersects(const AABB& other) const

		Returns true if the given AABB intersects with this, false otherwise.

	.. function:: bool Contains(const Vector3 &position) const

		Returns true if the given position lays within this, false otherwise.

Members
=======

.. class:: AABB

	.. member:: Vector3 position

		The position of the bounding box in world space.

	.. member:: Vector3 minExtend

		The position of the smallest x, y and z values of of the bounding box relative to its position.

	.. member:: Vector3 maxExtend

		The position of the biggest x, y and z values of of the bounding box relative to its position.

