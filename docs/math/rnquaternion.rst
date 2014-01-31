.. _renquaternion.rst:

**************************
Quaternion class reference
**************************

.. namespace:: RN
.. class:: Quaternion

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNMatrixQuaternion.h                 |
+---------------------+--------------------------------------+

Overview
========

.. inheritance_diagram::

The quaternion class implements a quaternion meant for storing rotations. The quaternions real part is represented by its `w` component and the three imaginary parts by the `x`, `y` and `z` components.
Quaternions are internally used for all rotations and offer interfaces to convert from and to yaw-pitch-roll angles, axis-angle and rotation matrix.
Yaw-pitch-roll angles are applied as y-x-z, meaning the yaw rotation around the y axis is being applied first, the pitch rotation around the new (with the previous rotation applied) x axis second and the roll rotation around the new z axis last.
Rotations represented by quaternions can be combined by multiplying the quaternions, the result is that of the first quaternions rotation applied first and then the seconds.
Also the + and - operators can be used to add or substract euler angles to or from the quaternion as if it was an euler angle itself.

Tasks
=====

Construction
------------

* :cpp:func:`Quaternion() <Quaternion::Quaternion>`
* :cpp:func:`Quaternion(float x, float y, float z, float w) <Quaternion::Quaternion>`
* :cpp:func:`Quaternion(const Vector3& euler) <Quaternion::Quaternion>`
* :cpp:func:`Quaternion(const Vector4& axisangle) <Quaternion::Quaternion>`
* :cpp:func:`WithIdentity() <Quaternion::WithIdentity>`
* :cpp:func:`WithEulerAngle(const Vector3& euler) <Quaternion::WithEulerAngle>`
* :cpp:func:`WithAxisAngle(const Vector4& axisangle) <Quaternion::WithAxisAngle>`
* :cpp:func:`WithLerpSpherical(const Quaternion& start, const Quaternion& end, float factor) <Quaternion::WithLerpSpherical>`
* :cpp:func:`WithLerpLinear(const Quaternion& start, const Quaternion& end, float factor) <Quaternion::WithLerpLinear>`
* :cpp:func:`WithLookAt(const Vector3& dir, const Vector3& up=Vector3(0.0f, 1.0f, 0.0f), bool forceup=false) <Quaternion::WithLookAt>`

  
Comparison
----------

* :cpp:func:`operator== (const Quaternion& other) const <Quaternion::operator==>`
* :cpp:func:`operator!= (const Quaternion& other) const <Quaternion::operator!=>`
* :cpp:func:`IsEqual(const Quaternion& other, float epsilon) const <Quaternion::IsEqual>`

  
Binary operators
----------------

* :cpp:func:`operator+ (const Quaternion& other) const <Quaternion::operator+>`
* :cpp:func:`operator- (const Quaternion& other) const <Quaternion::operator->`
* :cpp:func:`operator* (const Quaternion& other) const <Quaternion::operator*>`
* :cpp:func:`operator* (const float n) const <Quaternion::operator*>`
* :cpp:func:`operator/ (const Quaternion& other) const <Quaternion::operator/>`
* :cpp:func:`operator/ (const float n) const <Quaternion::operator/>`
* :cpp:func:`operator+= (const Quaternion& other) <Quaternion::operator+=>`
* :cpp:func:`operator-= (const Quaternion& other) <Quaternion::operator-=>`
* :cpp:func:`operator*= (const Quaternion& other) <Quaternion::operator*=>`
* :cpp:func:`operator*= (const float n) const <Quaternion::operator*=>`
* :cpp:func:`operator/= (const Quaternion& other) <Quaternion::operator/=>`
* :cpp:func:`operator/= (const float n) const <Quaternion::operator/=>`
* :cpp:func:`operator+ (const Vector3& other) const <Quaternion::operator+>`
* :cpp:func:`operator- (const Vector3& other) const <Quaternion::operator->`
* :cpp:func:`operator+= (const Vector3& other) <Quaternion::operator+=>`
* :cpp:func:`operator-= (const Vector3& other) <Quaternion::operator-=>`


Accessors
---------

* :cpp:func:`GetEulerAngle() const <Quaternion::GetEulerAngle>`
* :cpp:func:`GetAxisAngle() const <Quaternion::GetAxisAngle>`
* :cpp:func:`GetRotationMatrix() const <Quaternion::GetRotationMatrix>`
* :cpp:func:`GetLength() const <Quaternion::GetLength>`
* :cpp:func:`GetDotProduct(const Quaternion& other) const <Quaternion::GetDotProduct>`
* :cpp:func:`GetLerpSpherical(const Quaternion& other, float factor) const <Quaternion::GetLerpSpherical>`
* :cpp:func:`GetLerpLinear(const Quaternion& other, float factor) const <Quaternion::GetLerpLinear>`
 
Mutation
--------

* :cpp:func:`Normalize() <Quaternion::Normalize>`
* :cpp:func:`GetNormalized() <Quaternion::GetNormalized> const`
* :cpp:func:`Conjugate() <Quaternion::Conjugate>`
* :cpp:func:`GetConjugated() <Quaternion::GetConjugated> const`


Utility
-------

* :cpp:func:`GetRotatedVector(const Vector3& vec) const <Quaternion::GetRotatedVector>`
* :cpp:func:`GetRotatedVector(const Vector4& vec) const <Quaternion::GetRotatedVector>`


Instance Methods
================

.. class:: Quaternion 

	.. function:: Quaternion()

		Initializes the quaternion representing no rotation, setting the `x`, `y` and `z` parts to 0.0f and the `w` part to 1.0f.

	.. function:: Quaternion(float x, float y, float z, float w)

		Initializes the quaternion with the given values for the components.

	.. function:: Quaternion(const Vector3& euler)

		Initializes the quaternion with the given euler angles in degrees with x-y-z representing yaw-pitch-roll.

	.. function:: Quaternion(const Vector4& axisangle)

		Initializes the quaternion with the given axis-angle with `x`, `y` and `z` representing the axis and w the angle in degrees.

	.. function:: static Matrix WithIdentity()

		Returns an identity quaternion representing no rotation, setting the `x`, `y` and `z` parts to 0.0f and the `w` part to 1.0f.

	.. function:: static Matrix WithEulerAngle(const Vector3& euler)

		Returns a quaternion initialized with the rotation given as yaw-pitch-roll angles in degrees.

	.. function:: static Matrix WithAxisAngle(const Vector4& axisangle)

		Returns a quaternion initialized with the rotation given as axis values and an angle in degrees.
	


* :cpp:func:`WithLerpSpherical(const Quaternion& start, const Quaternion& end, float factor) <Quaternion::WithLerpSpherical>`
* :cpp:func:`WithLerpLinear(const Quaternion& start, const Quaternion& end, float factor) <Quaternion::WithLerpLinear>`
* :cpp:func:`WithLookAt(const Vector3& dir, const Vector3& up=Vector3(0.0f, 1.0f, 0.0f), bool forceup=false) <Quaternion::WithLookAt>`


	.. function:: bool operator== (const Matrix& other) const

		Compares the matrix against the other and returns `true` if they are deemed equal.
		This function is equivalent to calling `IsEqual(other, k::EpsilonFloat)`

	.. function:: bool operator!= (const Matrix& other) const

		Compares the matrix against the other and returns `true` if they are deemed unequal.
		This function is equivalent to calling `!IsEqual(other, k::EpsilonFloat)`

	.. function:: bool IsEqual(const Matrix& other, float epsilon) const

		Compares the matrix against the other using the provided epsilon. The function will subtract
		each component of the respective component of the other vector and compares them against the delta.
		If one exceeds the delta, the two vectors are deemed unequal and the function returns false.

	.. function:: Matrix operator* (const Matrix& other) const

		Returns a new matrix which is the result of the matrix multiplication of `this` and the `other` matrix.

	.. function:: Vector3 operator* (const Vector3& other) const

		Returns a new vector which is the vector transformed with the matrix, achieved by assuming the vectors missing fourth component to be 1 and multiplying the matrix with the vector.

	.. function:: Vector4 operator* (const Vector4& other) const

		Returns a new vector which is the vector transformed with the matrix by multiplying it with the vector.

	.. function:: Vector4& operator*= (const Vector4& other)

		Multiplies this matrix with the `other` matrix.

		:return: Reference to the mutated vector

	.. function:: Vector3 GetEulerAngle() const

		Returns a vector with yaw-pitch-roll angles interpreting the matrix as a rotation matrix without any modifications.

	.. function:: Vector4 GetAxisAngle() const

		Returns a vector with axis-angle representation interpreting the matrix as a rotation matrix without any modifications.

	.. function:: Quaternion GetQuaternion() const

		Returns a rotation quaternion interpreting the matrix as a rotation matrix without any modifications.

	.. function:: float GetDeterminant() const

		Returns the determinant of the matrix. The determinant is a single value providing some information about the matrix and is for example used to calculate the inverse matrix.

	.. function:: void Translate(const Vector3& translation)

		Multiplies the matrix with a matrix representing the given translation.

	.. function:: void Translate(const Vector4& translation)

		Multiplies the matrix with a matrix representing the given translation.

	.. function:: void Scale(const Vector3& scaling)

		Multiplies the matrix with a matrix representing the given scaling.

	.. function:: void Scale(const Vector4& scaling)

		Multiplies the matrix with a matrix representing the given scaling.

	.. function:: void Rotate(const Vector3& rotation)

		Multiplies the matrix with a matrix representing the given rotation interpreted as yaw-pitch-roll angles in degrees.

	.. function:: void Rotate(const Vector3& rotation)

		Multiplies the matrix with a matrix representing the given rotation interpreted as an axis with an angle in degrees.

	.. function:: void Rotate(const Quaternion& rotation)

		Multiplies the matrix with a matrix representing the given rotation from the quaternion.

	.. function:: void Transpose()

		Transposes the matrix, this means that its previous rows are now columns. So the value from m[1] (first column, second row) is for example in m[4] (second column, first row) afterwards.
		For rotation and scaling matrices and other orthogonal matrices this is the same as the inverse.

	.. function:: Matrix GetTransposed()

		Returns the transposed matrix, this means that its rows are the new matrices columns. So the value from m[1] (first column, second row) is for example in m[4] (second column, first row) afterwards.
		For rotation and scaling matrices and other orthogonal matrices this is the same as the inverse.

	.. function:: void Inverse() const

		Inverts this matrix.

	.. function:: Matrix GetInverse() const

		Returns the inverse of this matrix. The inverse is defined as the matrix to multiply the receiver with to get the identity matrix.

Members
=======

.. class:: Matrix

	.. member:: float x

		The first imaginary part of the quaternion.

	.. member:: float y

		The second imaginary part of the quaternion.

	.. member:: float z

		The third imaginary part of the quaternion.

	.. member:: float w

		The real part of the quaternion.

