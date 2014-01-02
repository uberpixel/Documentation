.. _rnconstants.rst:

*******************
Constants reference
*******************

.. namespace:: RN

+-----------------+--------------+
| **Declared in** | RNCostants.h |
+-----------------+--------------+

Overview
========

This document describes the constants found in Rayne. All constants live in the `k` namespace within the `RN` namespace.

Constants
=========

.. member:: static const float k::Pi
	
	Holds the value of pi.

.. member:: static const float k::Pi_2

	Holds the value of pi divided by 2.

.. member:: static const float k::Pi_4
	
	Holds the value of pi divided by 4

.. member:: static const float k::E
	
	Holds the base of natural logarithms.

.. member:: static const float k::Log2E

	Holds the base-2 logarithm of e

.. member:: static const float k::Log10E

	Holds the base-10 logarithm of e

.. member:: static const float k::Sqrt2

	Holds the positive square root of 2

.. member:: static const float k::Sqrt1_2

	Holds the positive square root of 1/2

.. member:: static const float k::EpsilonFloat

	Holds the smallest positive number such that :code:`1.0f + k::EpsilonFloat != 1.0f`. Should be used to compare floating
	point variables with each other (eg: :code:`Math::FastAbs(a - b) < k::EpsilonFloat`)

.. member:: static const size_t k::NotFound

	Symbolic index to signal that something couldn't be found. For example, the :cpp:class:`Array` class returns
	this value for operations such as :cpp:func:`Array::IndexOfObject` when it can't find the given object.

.. c:macro:: kRNNotFound
	
	Shorthand for :cpp:member:`k::NotFound`
