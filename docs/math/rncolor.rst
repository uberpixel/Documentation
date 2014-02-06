.. _rncolor.rst:

***********************
Color class reference
***********************

.. namespace:: RN
.. class:: Color

+---------------------+--------------------------------------+
|   **Availability**  |              Rayne 1.0               |
+---------------------+--------------------------------------+
| **Declared in**     | RNColor.h                            |
+---------------------+--------------------------------------+

Overview
========

The Color class provides a four component floating point rgba color implementation.

Tasks
=====

Construction
------------

* :cpp:func:`Color(float n=1.0f) <Color::Color>`
* :cpp:func:`Color(float r, float g, float b, float a=1.0f) <Color::Color>`
* :cpp:func:`Color(int r, int g, int b, int a=255) <Color::Color>`

* :cpp:func:`Red() <Color::Red>`
* :cpp:func:`Green() <Color::Green>`
* :cpp:func:`Blue() <Color::Blue>`
* :cpp:func:`Yellow() <Color::Yellow>`
* :cpp:func:`Black() <Color::Black>`
* :cpp:func:`White() <Color::White>`
* :cpp:func:`Gray() <Color::Gray>`
* :cpp:func:`ClearColor() <Color::ClearColor>`
  
Comparison
----------

* :cpp:func:`operator== (const Color& other) const <Color::operator==>`
* :cpp:func:`operator!= (const Color& other) const <Color::operator!=>`

Unary operators
---------------

* :cpp:func:`operator- () const <Color::operator->`
  
Binary operators
----------------

* :cpp:func:`operator+ (const Color& other) const <Color::operator+>`
* :cpp:func:`operator+ (const float n) const <Color::operator+>`
* :cpp:func:`operator- (const Color& other) const <Color::operator->`
* :cpp:func:`operator- (const float n) const <Color::operator->`
* :cpp:func:`operator* (const Color& other) const <Color::operator*>`
* :cpp:func:`operator* (const float n) const <Color::operator*>`
* :cpp:func:`operator/ (const Color& other) const <Color::operator/>`
* :cpp:func:`operator/ (const float n) const <Color::operator/>`
* :cpp:func:`operator+= (const Color& other) <Color::operator+=>`
* :cpp:func:`operator+= (const float n) <Color::operator+=>`
* :cpp:func:`operator-= (const Color& other) <Color::operator-=>`
* :cpp:func:`operator-= (const float n) <Color::operator-=>`
* :cpp:func:`operator*= (const Color& other) <Color::operator*=>`
* :cpp:func:`operator*= (const float n) <Color::operator*=>`
* :cpp:func:`operator/= (const Color& other) <Color::operator/=>`
* :cpp:func:`operator/= (const float n) <Color::operator/=>`

  
Instance Methods
================

.. class:: Color 

	.. function:: Color(float n=1.0f)

		Initializes all four components with the value of n.

	.. function:: Color(float r, float g, float b, float a=1.0f)

		Initializes each component with the value given by the parameter with the same name.

	.. function:: Color(int r, int g, int b, int a=255)

		Initializes each component with the value given by the parameter with the same name scaled with a factor of 1/255.

	.. function:: static Color Red()

		Returns a red color, which means that the `r` and the `a` components are 1.0f and the others are 0.0f.

	.. function:: static Color Green()

		Returns a green color, which means that the `g` and the `a` components are 1.0f and the others are 0.0f.

	.. function:: static Color Blue()

		Returns a blue color, which means that the `b` and the `a` components are 1.0f and the others are 0.0f.

	.. function:: static Color Yellow()

		Returns a yellow color, which means that the `r`, `g` and the `a` components are 1.0f and the others are 0.0f.

	.. function:: static Color Black()

		Returns a black color, which means that all but the `a` component are 0.0f, the `a` component is 1.0f.

	.. function:: static Color White()

		Returns a white color, which means that all components are 1.0f.

	.. function:: static Color Gray()

		Returns a grey color, which means that the `r`, `g` and `b` components are 0.5f and the `a` component is 1.0f.

	.. function:: static Color ClearColor()

		Returns a transparent black color, which means that all components are 0.0f.

	.. function:: bool operator== (const Color& other) const

		Compares the color against the other and returns `true` if they are deemed equal.

	.. function:: bool operator!= (const Color& other) const

		Compares the color against the other and returns `true` if they are deemed unequal.

	.. function:: Color operator- () const

		Returns a new color with its components negated.

	.. function:: Color operator+ (const Color& other) const

		Returns a new color with all components of the `other` color added to the components of `this`.

	.. function:: Color operator+ (const float n) const

		Returns a new color with `n` added to all components of `this`.

	.. function:: Color operator- (const Color& other) const

		Returns a new color with all components of the `other` color subtracted from the components of `this`.

	.. function:: Color operator- (const float n) const

		Returns a new color with `n` subtracted from all components of `this`.

	.. function:: Color operator* (const Color& other) const

		Returns a new color with all components of `this` multiplied with the components of the `other` color.

	.. function:: Color operator* (const float n) const

		Returns a new color with all components of `this` multiplied with `n`.

	.. function:: Color operator/ (const Color& other) const

		Returns a new color with all components of `this` divided by the components of the `other` color.

	.. function:: Color operator/ (const float n) const

		Returns a new color with all components of `this` divided by `n`.

	.. function:: Color& operator+= (const Color& other)

		Adds the components of the `other` color to the respective components of the color.

		:return: Reference to the mutated color

	.. function:: Color& operator+= (const float n)

		Adds `n` to all components of the color.

		:return: Reference to the mutated color

	.. function:: Color& operator-= (const Color& other)

		Subtracts the components of the `other` color from the respective components of the color.

		:return: Reference to the mutated color

	.. function:: Color& operator-= (const float other)

		Subtracts `n` from all components of the color.

		:return: Reference to the mutated color

	.. function:: Color& operator*= (const Color& other)

		Multiplies the components of the `other` color with the respective components of the color.

		:return: Reference to the mutated color

	.. function:: Color& operator*= (const float other)

		Multiplies all components of the color with `n`.

		:return: Reference to the mutated color

	.. function:: Color& operator/= (const Color& other)

		Divides the components of the `other` color by the respective components of the color.

		:return: Reference to the mutated color

	.. function:: Color& operator/= (const float other)

		Divides all components of the color by `n`.

		:return: Reference to the mutated color


Members
=======

.. class:: Color

	.. member:: float r

		The red component of the color

	.. member:: float g

		The green component of the color

	.. member:: float b

		The blue component of the color

	.. member:: float a

		The alpha component of the color

