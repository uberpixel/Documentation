.. _renvector4.rst:

***********************
Matrix class reference
***********************

.. namespace:: RN
.. class:: Matrix

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNMatrix.h                           |
+---------------------+--------------------------------------+

Overview
========

.. inheritance_diagram::

The Matrix class provides a 4x4 column major matrix implementation. This class is mostly used to store transformation (translation, rotation and scaling) information for scene nodes needed for rendering and parent-child relations.
SIMD will be used if supported.

Tasks
=====

Construction
------------

* :cpp:func:`Matrix() <Matrix::Matrix>`
* :cpp:func:`WithIdentity() <Matrix::WithIdentity>`
* :cpp:func:`WithTranslation(const Vector3& translation) <Matrix::WithTranslation>`
* :cpp:func:`WithTranslation(const Vector4& translation) <Matrix::WithTranslation>`
* :cpp:func:`WithScaling(const Vector3& scaling) <Matrix::WithScaling>`
* :cpp:func:`WithScaling(const Vector4& scaling) <Matrix::WithScaling>`
* :cpp:func:`WithRotation(const Vector3& rotation) <Matrix::WithRotation>`
* :cpp:func:`WithRotation(const Vector4& rotation) <Matrix::WithRotation>`
* :cpp:func:`WithRotation(const Quaternion& rotation) <Matrix::WithRotation>`
* :cpp:func:`WithProjectionOrthogonal(float left, float right, float bottom, float top, float clipnear, float clipfar) <Matrix::WithProjectionOrthogonal>`
* :cpp:func:`WithProjectionPerspective(float arc, float aspect, float clipnear, float clipfar) <Matrix::WithProjectionPerspective>`
* :cpp:func:`WithInverseProjectionPerspective(float arc, float aspect, float clipnear, float clipfar) <Matrix::WithInverseProjectionPerspective>`

  
Comparison
----------

* :cpp:func:`operator== (const Matrix& other) const <Matrix::operator==>`
* :cpp:func:`operator!= (const Matrix& other) const <Matrix::operator!=>`
* :cpp:func:`IsEqual(const Matrix& other, float epsilon) const <Matrix::IsEqual>`

  
Binary operators
----------------

* :cpp:func:`operator* (const Matrix& other) const <Matrix::operator*>`
* :cpp:func:`operator* (const Vector3& other) const <Matrix::operator*>`
* :cpp:func:`operator* (const Vector4& other) const <Matrix::operator*>`
* :cpp:func:`operator*= (const Matrix& other) <Matrix::operator*=>`

Accessors
---------

* :cpp:func:`GetEulerAngle() const <Matrix::GetEulerAngle>`
* :cpp:func:`GetQuaternion() const <Matrix::GetQuaternion>`
* :cpp:func:`GetDeterminant() const <Matrix::GetDeterminant>`

 
Mutation
--------

* :cpp:func:`Translate(const Vector3& translation) <Matrix::Translate>`
* :cpp:func:`Translate(const Vector4& translation) <Matrix::Translate>`
* :cpp:func:`Scale(const Vector3& scaling) <Matrix::Scale>`
* :cpp:func:`Scale(const Vector4& scaling) <Matrix::Scale>`
* :cpp:func:`Rotate(const Vector3& rotation) <Matrix::Rotate>`
* :cpp:func:`Rotate(const Vector4& rotation) <Matrix::Rotate>`
* :cpp:func:`Rotate(const Quaternion& rotation) <Matrix::Rotate>`
* :cpp:func:`Transpose() <Matrix::Transpose>`
* :cpp:func:`GetTransposed() <Matrix::GetTransposed>`
* :cpp:func:`Inverse() <Matrix::Inverse>`
* :cpp:func:`GetInverse() <Matrix::GetInverse>`


Instance Methods
================

.. class:: Matrix 

	.. function:: Matrix()

		Initializes the matrix as an identity matrix, setting the values `m[0]`, `m[5]`, `m[10]` and `m[15]` to 1.0f and all others to 0.0f.

	.. function:: static Matrix WithIdentity()

		Returns an identity matrix with the values `m[0]`, `m[5]`, `m[10]` and `m[15]` set to 1.0f and all others to 0.0f.
	
	.. function static Matrix WithTranslation(const Vector3& translation)

		Returns a translation matrix, which is an identity matrix with the fourth column set to the values of the vector. Transforming a vector with this will add those values to that vector.

	.. function static Matrix WithTranslation(const Vector4& translation)

		Returns a translation matrix, which is an identity matrix with the fourth column set to the values of the vector. Transforming a vector with this will add those values to that vector.

	.. function static Matrix WithScaling(const Vector3& scaling)

		Returns an identity matrix with the scaling values instead of the 1.0f values. Transforming a vector with this, will result in a component wise multiplication of that vector with the scaling vector.

	.. function static Matrix WithScaling(const Vector4& scaling)

		Returns an identity matrix with the scaling values instead of the 1.0f values. Transforming a vector with this, will result in a component wise multiplication of that vector with the scaling vector.

	.. function static Matrix WithRotation(const Vector3& rotation)

		Returns a rotation matrix with the parameters x, y and z values interpreted as yaw, pitch and roll angles in degrees. They are combined in this order: yaw, pitch, roll. Yaw is the rotation around the worlds y-axis, pitch the rotation around the new x-axis and roll the rotation around the new z-axis.
		Transforming a vector with it will rotate it in exactly that order.

	.. function static Matrix WithRotation(const Vector4& rotation)

		Returns a rotation matrix with the parameter interpreted as axis-angle values, meaning that its `x`, `y` and `z` values are interpreted as an axis and the `w` value as the rotation angle around that axis.

	.. function static Matrix WithRotation(const Quaternion& rotation)

		Returns a rotation matrix from the rotation represented by the quaternion given as parameter.

	.. function static Matrix WithProjectionOrthogonal(float left, float right, float bottom, float top, float clipnear, float clipfar)

		Returns an orthogonal projection matrix from the given parameters. This is just a scaling matrix scaling from the box given by the parameters to a new box with its borders ranging from -1.0f to 1.0f.

	.. function static Matrix WithProjectionPerspective(float arc, float aspect, float clipnear, float clipfar)

		Returns a perspective projection matrix from the given parameters. It will scale vectors with -z approaching clipfar much smaller than a -z closer to clipnear depending on the arc and aspect parameters. The arc value is interpreted as an angle in degrees.

	.. function static Matrix WithInverseProjectionPerspective(float arc, float aspect, float clipnear, float clipfar)

		Returns an inverse perspective projection matrix from the given parameters.


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

	.. member:: float m[16]

		The values of the matrix aligned like this:

			+--+--+--+--+
			| 0| 4| 8|12|
			+--+--+--+--+
			| 1| 5| 9|13|
			+--+--+--+--+
			| 2| 6|10|14|
			+--+--+--+--+
			| 3| 7|11|15|
			+--+--+--+--+