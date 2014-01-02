.. _renvector2.rst:

***********************
Vector2 class reference
***********************

.. namespace:: RN
.. class:: Vector2 

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNVector.h                           |
+---------------------+--------------------------------------+

Overview
========

The Vector2 class provides a 2d floating point vector implementation. Vector2 is trivially copyable.

Tasks
=====

Construction
------------

* :cpp:func:`Vector2() <Vector2::Vector2>`
* :cpp:func:`Vector2(float n) <Vector2::Vector2>`
* :cpp:func:`Vector2(float x, float y) <Vector2::Vector2>`
* :cpp:func:`Vector2(const Vector3& other) explicit <Vector2::Vector2>`
* :cpp:func:`Vector2(const Vector4& other) explicit <Vector2::Vector2>`
  
Comparison
----------

* :cpp:func:`operator== (const Vector2& other) const <Vector2::operator==>`
* :cpp:func:`operator!= (const Vector2& other) const <Vector2::operator!=>`
* :cpp:func:`IsEqual(const Vector2& other, float epsilon) const <Vector2::IsEqual>`

Unary operators
---------------

* :cpp:func:`operator- () const <Vector2::operator->`
  
Binary operators
----------------

* :cpp:func:`operator+ (const Vector2& other) const <Vector2::operator+>`
* :cpp:func:`operator- (const Vector2& other) const <Vector2::operator->`
* :cpp:func:`operator* (const Vector2& other) const <Vector2::operator*>`
* :cpp:func:`operator/ (const Vector2& other) const <Vector2::operator/>`
* :cpp:func:`operator* (const float n) const <Vector2::operator*>`
* :cpp:func:`operator/ (const float n) const <Vector2::operator/>`
* :cpp:func:`operator+= (const Vector2& other) <Vector2::operator+=>`
* :cpp:func:`operator-= (const Vector2& other) <Vector2::operator-=>`
* :cpp:func:`operator*= (const Vector2& other) <Vector2::operator*=>`
* :cpp:func:`operator/= (const Vector2& other) <Vector2::operator/=>`

Accessors
---------

* :cpp:func:`Length() const <Vector2::Length>`
* :cpp:func:`Dot(const Vector2& other) const <Vector2::Dot>`
 
Mutation
--------

* :cpp:func:`Normalize(float n) <Vector2::Normalize>`

Instance Methods
================

.. class:: Vector2 

	.. function:: Vector2()

		Initializes the `x` and `y` component to `0.0f`

	.. function:: Vector2(float n)

		Initializes the `x` and `y` component to the value in `n`

	.. function:: Vector2(float x, float y)

		Initializes the `x` and `y` component to the `x` and `y` parameters respectively

	.. function:: Vector2(const Vector3& other)

		Initialized the `x` and `y` component to the `x` and `y` components of the `other` vector

	.. function:: Vector2(const Vector4& other)

		Initialized the `x` and `y` component to the `x` and `y` components of the `other` vector

	.. function:: bool operator== (const Vector2& other) const

		Compares the vector against the other and returns `true` if they are deemed equal.
		This function is equivalent to calling `IsEqual(other, k::EpsilonFloat)`

	.. function:: bool operator!= (const Vector2& other) const

		Compares the vector against the other and returns `true` if they are deemed unequal.
		This function is equivalent to calling `!IsEqual(other, k::EpsilonFloat)`

	.. function:: bool IsEqual(const Vector2& other, float epsilon) const

		Compares the vector against the other using the provided epsilon. The function will subtract
		each component of the respective component of the other vector and compares them against the delta.
		If one exceeds the delta, the two vectors are deemed unequal and the function returns false.

	.. function:: Vector2 operator- () const

		Returns a new vector with its components negated.

	.. function:: Vector2 operator+ (const Vector2& other) const

		Returns a new vector with all components of the `other` vector added to the components of `this`

	.. function:: Vector2 operator- (const Vector2& other) const

		Returns a new vector with all components of the `other` vector subtracted from the components of `this`

	.. function:: Vector2 operator* (const Vector2& other) const

		Returns a new vector with all components of `this` multiplied with the components of the `other` vector

	.. function:: Vector2 operator/ (const Vector2& other) const

		Returns a new vector with all components of `this` divided by the components of the `other` vector

	.. function:: Vector2 operator* (const float n) const

		Returns a new vector with all components of `this` multiplied with `n`

	.. function:: Vector2 operator/ (const float n) const

		Returns a new vector with all components of `this` divided by `n`

	.. function:: Vector2& operator+= (const Vector2& other)

		Adds the components of the `other` vector to the respective components of the vector

		:return: Reference to the mutated vector

	.. function:: Vector2& operator-= (const Vector2& other)

		Subtracts the components of the `other` vector from the respective components of the vector

		:return: Reference to the mutated vector

	.. function:: Vector2& operator*= (const Vector2& other)

		Multiplies the components of the `other` vector with the respective components of the vector

		:return: Reference to the mutated vector

	.. function:: Vector2& operator/= (const Vector2& other)

		Divides the components of the `other` vector by the respective components of the vector

		:return: Reference to the mutated vector

	.. function:: float Length() const

		Returns the length of the vector

	.. function:: float Dot(const Vector2& other) const

		Returns the dot product of the vector and the `other` vector

	.. function:: Vector2& Normalize(const float n)

		Normalizes the vector to the constant `n`

		:return: Reference to the mutated vector

Member
======

.. class:: Vector2

	.. member:: float x

		The x component of the vector

	.. member:: float y

		The y component of the vector
