.. _rnplane.rst:

*********************
Plane class reference
*********************

.. namespace:: RN
.. class:: Plane 

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNPlane.h                            |
+---------------------+--------------------------------------+

Overview
========

The plane class implements an endless plane in three dimensional space as a normal and a position and functionality to determine the distance of points to the plane.

Tasks
=====

Construction
------------

* :cpp:func:`Plane() <Plane::Plane>`
* :cpp:func:`WithPositionNormal(const Vector3 &position, const Vector3 &normal) <Plane::WithPositionNormal>`
* :cpp:func:`WithTriangle(const Vector3 &position1, const Vector3 &position2, const Vector3 &position3, float dirfac=1.0f) <Plane::WithTriangle>`


Accessors
---------

* :cpp:func:`SetPosition(const Vector3 &position) <Plane::SetPosition>`
* :cpp:func:`SetNormal(const Vector3 &normal) <Plane::SetNormal>`
* :cpp:func:`GetPosition() const <Plane::GetPosition>`
* :cpp:func:`GetNormal() const <Plane::GetNormal>`
* :cpp:func:`GetD() const <Plane::GetD>`
* :cpp:func:`GetDistance(const Vector3 &position) const <Plane::GetDistance>`
 

Instance Methods
================

.. class:: Plane 

	.. function:: Plane()

		Initializes the normal as (0, 1, 0) and the position as (0, 0, 0).

	.. function:: Plane WithPositionNormal(const Vector3 &position, const Vector3 &normal)

		Returns a new plane initialized with the given position and normal.

	.. function:: Plane WithTriangle(const Vector3 &position1, const Vector3 &position2, const Vector3 &position3, float dirfac=1.0f)

		Returns a new plane initialized with the plane going through the three given points. dirfac can be used to flip the normal.

	.. function:: void SetPosition(const Vector3 &position)

		Sets the position of the plane.

	.. function:: void SetNormal(const Vector3 &normal)

		Sets the normal of the plane.

	.. function:: Vector3 GetPosition() const

		Returns the planes position.

	.. function:: Vector3 GetNormal() const

		Returns the planes normal.

	.. function:: Vector3 GetD() const

		Returns d, which is the result of the dot product of position and normal and is for example used to determine a points distance to the plane.

	.. function:: float GetDistance(Vector3& position) const

		Returns the distance of the position to the plane. It is 0 if it lays on the plane, negative if it is below the plane or positive if it is above the plane.
		