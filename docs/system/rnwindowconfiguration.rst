.. _rnwindowconfiguration.rst:

***********************************
WindowConfiguration class reference
***********************************

.. namespace:: RN
.. class:: WindowConfiguration

+-------------------+---------------------+
| **Inherits from** | :cpp:class:`Object` |
+-------------------+---------------------+
| **Availability**  | Rayne 1.0           |
+-------------------+---------------------+
| **Declared in**   | RNWindow.h          |
+-------------------+---------------------+
| **Meta Traits**   | `Copyable`          |
+-------------------+---------------------+

Overview
========

The WindowConfiguration encapsulates a pixel resolution and :cpp:class:`screen <Screen>`. It's used in conjunction with the :cpp:class:`Window` class to allow resolution and screen changes of the rendering window. Window configurations are implicitly or explicitly bound to a screen, and their resolution is automatically clamped to the maximum resolution of the screen.

Tasks
=====

Creation
--------

* :cpp:func:`WindowConfiguration(uint32 width, uint32 height) <WindowConfiguration::WindowConfiguration>`
* :cpp:func:`WindowConfiguration(uint32 width, uint32 height, Screen *screen) <WindowConfiguration::WindowConfiguration>`

Properties
----------

* :cpp:func:`GetWidth() const <WindowConfiguration::GetWidth>`
* :cpp:func:`GetHeight() const <WindowConfiguration::GetHeight>`
* :cpp:func:`GetScreen() const <WindowConfiguration::GetScreen>`


Instance Methods
================

.. class:: WindowConfiguration
	
	.. function:: WindowConfiguration(uint32 width, uint32 height)

		Constructor for a new window configuration that is bound to the main screen.

	.. function:: WindowConfiguration(uint32 width, uint32 height, Screen *screen)

		Constructor for a new window configuration that is bound to the given screen

	.. function:: uint32 GetWidth() const

		Returns the width for the configuration

	.. function:: uint32 GetHeight() const

		Returns the height for the configuration

	.. function:: Screen *GetScreen() const

		Returns the screen for the configuration
