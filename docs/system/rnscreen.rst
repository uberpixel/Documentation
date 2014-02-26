.. _rnscreen.rst:

**********************
Screen class reference
**********************

.. namespace:: RN
.. class:: Screen

+-------------------+------------+
| **Inherits from** |   None     |
+-------------------+------------+
| **Availability**  | Rayne 1.0  |
+-------------------+------------+
| **Declared in**   | RNWindow.h |
+-------------------+------------+

Overview
========

The Screen class encapsulates a physical display device attached to the users computer. It allows access to the various window configurations supported by the device, as well as access to the frame of the device within the virtual workspace.

Tasks
=====

Properties
----------

* :cpp:func:`GetWidth() const <Screen::GetWidth>`
* :cpp:func:`GetHeight() const <Screen::GetHeight>`
* :cpp:func:`GetScaleFactor() const <Screen::GetScaleFactor>`
* :cpp:func:`GetFrame() const <Screen::GetFrame>`
* :cpp:func:`GetConfigurations() const <Screen::GetConfigurations>`

Instance Methods
================

.. class:: Screen
	
	.. function:: uint32 GetWidth() const

		Returns the width of the screen in pixels

	.. function:: uint32 GetHeight() const

		Returns the height of the screen in pixels

	.. function:: float GetScaleFactor() const

		Returns the scale factor of the screen. This value determines the conversion rate between points and pixels, and is 1.0 for normal displays and 1.5 or greater for high resolution displays.

	.. function:: const Rect &GetFrame() const

		Returns the frame of the screen within the virtual work space. The size of the frame is identical to the reported width and height, the position for the main display is typically `0|0`, but other values are also possible.

	.. function:: const Array *GetConfigurations() const

		Returns an array of :cpp:class:`WindowConfiguration` objects with the supported resolution settings for the screen.
