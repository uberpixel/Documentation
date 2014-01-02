.. _renvector3.rst:

***********************
Vector3 class reference
***********************

.. namespace:: RN
.. class:: Vector3

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNVector.h                           |
+---------------------+--------------------------------------+

Overview
========

.. inheritance_diagram::

The Vector3 class provides a 3d floating point vector implementation. Vector3 is trivially copyable.

Tasks
=====

Construction
------------

* :cpp:func:`Vector3() <Vector3::Vector3>`
* :cpp:func:`Vector3(float n) <Vector3::Vector3>`
* :cpp:func:`Vector3(float x, float y, float z) <Vector3::Vector3>`
* :cpp:func:`Vector3(const Vector3& other) explicit <Vector3::Vector3>`
* :cpp:func:`Vector3(const Vector2& other, float z = 0.0f) explicit <Vector3::Vector3>`
* :cpp:func:`Vector3(const Vector4& other) explicit <Vector3::Vector3>`
  
Comparison
----------

* :cpp:func:`operator== (const Vector3& other) const <Vector3::operator==>`
* :cpp:func:`operator!= (const Vector3& other) const <Vector3::operator!=>`
* :cpp:func:`IsEqual(const Vector3& other, float epsilon) const <Vector3::IsEqual>`

Unary operators
---------------

* :cpp:func:`operator- () const <Vector3::operator->`
  
Binary operators
----------------

* :cpp:func:`operator+ (const Vector3& other) const <Vector3::operator+>`
* :cpp:func:`operator- (const Vector3& other) const <Vector3::operator->`
* :cpp:func:`operator* (const Vector3& other) const <Vector3::operator*>`
* :cpp:func:`operator/ (const Vector3& other) const <Vector3::operator/>`
* :cpp:func:`operator* (const float n) const <Vector3::operator*>`
* :cpp:func:`operator/ (const float n) const <Vector3::operator/>`
* :cpp:func:`operator+= (const Vector3& other) <Vector3::operator+=>`
* :cpp:func:`operator-= (const Vector3& other) <Vector3::operator-=>`
* :cpp:func:`operator*= (const Vector3& other) <Vector3::operator*=>`
* :cpp:func:`operator/= (const Vector3& other) <Vector3::operator/=>`

Accessors
---------

* :cpp:func:`Length() const <Vector3::Length>`
* :cpp:func:`Dot(const Vector3& other) const <Vector3::Dot>`
* :cpp:func:`Cross(const Vector3& other) const <Vector3::Cross>`
* :cpp:func:`Distance(const Vector3& other) const <Vector3::Distance>`
* :cpp:func:`Lerp(const Vector3& other, float factor) const <Vector3::Lerp>`

 
Mutation
--------

* :cpp:func:`Normalize(float n) <Vector3::Normalize>`
  
Instance Methods
================

.. class:: Vector3 

	.. function:: Vector3()

		Initializes the `x`, `y` and `z` component to `0.0f`

	.. function:: Vector3(float n)

		Initializes the `x`, `y` and `z` component to the value in `n`

	.. function:: Vector3(float x, float y, float z)

		Initialized the `x`, `y` `z` component to the `x`, `y` and `z` parameters respectively

	.. function:: Vector3(const Vector3& other)

		Initialized the `x`, `y` `z` component to the `x`, `y` and `z` components of the `other` vector

	.. function:: Vector3(const Vector2& other, float z = 0.0f)

		Initialized the `x` and `y` component to the `x`, and `y` components of the `other` vector and the `z` component to `z`

	.. function:: Vector3(const Vector4& other)

		Initialized the `x`, `y` `z` component to the `x`, `y` and `z` components of the `other` vector

	.. function:: bool operator== (const Vector3& other) const

		Compares the vector against the other and returns `true` if they are deemed equal.
		This function is equivalent to calling `IsEqual(other, k::EpsilonFloat)`

	.. function:: bool operator!= (const Vector3& other) const

		Compares the vector against the other and returns `true` if they are deemed unequal.
		This function is equivalent to calling `!IsEqual(other, k::EpsilonFloat)`

	.. function:: bool IsEqual(const Vector3& other, float epsilon) const

		Compares the vector against the other using the provided epsilon. The function will subtract
		each component of the respective component of the other vector and compares them against the delta.
		If one exceeds the delta, the two vectors are deemed unequal and the function returns false.

	.. function:: Vector3 operator- () const

		Returns a new vector with its components negated.

	.. function:: Vector3 operator+ (const Vector3& other) const

		Returns a new vector with all components of the `other` vector added to the components of `this`

	.. function:: Vector3 operator- (const Vector3& other) const

		Returns a new vector with all components of the `other` vector subtracted from the components of `this`

	.. function:: Vector3 operator* (const Vector3& other) const

		Returns a new vector with all components of `this` multiplied with the components of the `other` vector

	.. function:: Vector3 operator/ (const Vector3& other) const

		Returns a new vector with all components of `this` divided by the components of the `other` vector

	.. function:: Vector3 operator* (const float n) const

		Returns a new vector with all components of `this` multiplied with `n`

	.. function:: Vector3 operator/ (const float n) const

		Returns a new vector with all components of `this` divided by `n`

	.. function:: Vector3& operator+= (const Vector3& other)

		Adds the components of the `other` vector to the respective components of the vector

		:return: Reference to the mutated vector

	.. function:: Vector3& operator-= (const Vector3& other)

		Subtracts the components of the `other` vector from the respective components of the vector

		:return: Reference to the mutated vector

	.. function:: Vector3& operator*= (const Vector3& other)

		Multiplies the components of the `other` vector with the respective components of the vector

		:return: Reference to the mutated vector

	.. function:: Vector3& operator/= (const Vector3& other)

		Divides the components of the `other` vector by the respective components of the vector

		:return: Reference to the mutated vector

	.. function:: float Length() const

		Returns the length of the vector

	.. function:: float Dot(const Vector3& other) const

		Returns the dot product of the vector and the `other` vector

	.. function:: Vector3 Cross(const Vector3& other) const

		Returns the cross product of the vector and the `other` vector

	.. function:: float Distance(const Vector3& other) const

		Returns the distance between this vector and the `other` vector

	.. function:: Vector3 Lerp(const Vector3& other, float factor) const

		Linearly interpolates between this vector and the `other` vector by the given `factor` and returns the result

	.. function:: Vector3& Normalize(const float n)

		Normalizes the vector to the constant `n`

		:return: Reference to the mutated vector

Member
======

.. class:: Vector3

	.. member:: float x

		The x component of the vector

	.. member:: float y

		The y component of the vector

	.. member:: float z

		The z component of the vector

