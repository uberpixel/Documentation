.. _rnmath.rst:

**********************
General math functions
**********************

.. namespace:: RN
.. namespace:: Math

+-----------------+--------------+
| **Declared in** | RNMath.h     |
+-----------------+--------------+

Overview
========

This document describes the general math functions found in Rayne. All methods here are in the `RN::Math` namespace.

Functions
=========

.. cpp:function:: float FastAbs(float val)
	
	Returns the absolute value of `val` in the fastest way possible

.. cpp:function:: double FastAbs(double val)
	
	Returns the absolute value of `val` in the fastest way possible

.. cpp:function:: bool IsNegative(float val)
	
	Returns wether `val` is negative or not in the fastest way possible by checking the sign bit.

.. cpp:function:: bool IsNegative(double val)
	
	Returns wether `val` is negative or not in the fastest way possible by checking the sign bit.

.. cpp:function:: bool Compare(float x, float y, float delta = k::EpsilonFloat)
	
	Compares the two floats against each other using the provided delta and returns true if they compare equal to each other,
	that is, `FastAbs(x - y) < delta` is true. Useful to compare floating point variables against each other.

.. cpp:function:: bool Compare(double x, double y, float delta = k::EpsilonFloat)

	Compares the two doubles against each other using the provided delta and returns true if they compare equal to each other,
	that is, `FastAbs(x - y) < delta` is true. Useful to compare floating point variables against each other.
	

.. cpp:function:: float RadiansToDegrees(float radians)
	
	Converts the given radians to degrees

.. cpp:function:: float DegreesToRadians(float degrees)
	
	Converts the given degress to radians


.. cpp:function:: float Sqrt(float x)
	
	Returns the square root for `x` as fast as possible. On systems with SIMD (SSE or NEON), Rayne will use an SIMD optimized version for the calculation.

.. cpp:function:: float InverseSqrt(float x)
	
	Returns the inverse square root for `x` as fast as possible. On systems with SIMD (SSE or NEON), Rayne will use an SIMD optimized version for the calculation.

.. cpp:function:: float Sin(float x)

	Returns the sine of `x`, where `x` is an angle in radians.

.. cpp:function:: float Cos(float x)

	Returns the cosine of `x`, where `x` is an angle in radians.