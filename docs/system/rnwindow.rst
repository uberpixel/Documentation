.. _rnwindow.rst:

**********************
Window class reference
**********************

.. namespace:: RN
.. class:: Window

+-------------------+------------------------------------------------+
| **Inherits from** | :cpp:class:`ISingleton\<Window\> <ISingleton>` |
+-------------------+------------------------------------------------+
| **Availability**  | Rayne 1.0                                      |
+-------------------+------------------------------------------------+
| **Declared in**   | RNWindow.h                                     |
+-------------------+------------------------------------------------+

Overview
========

The Window class, along with the auxiliary classes :cpp:class:`Screen` and :cpp:class:`WindowConfiguration`, provide access to the underlying operating systems window server as well as Rayne's appearance in there. It allows putting Rayne into fullscreen, have it run in a borderless window and enumerate displays as well as their configurations.

Multithreading note
-------------------

Though the Window class is thread safe, the underlying methods it uses are usually not. As a result, window operations are deferred to the main thread and executed with a frame delay if they are called from a background thread. Because of this, it may take a frame before the active configuration or screen are actually changed.


Tasks
=====

Appearance changes
------------------

* :cpp:func:`SetTitle(const std::string &title) <Window::SetTitle>`
* :cpp:func:`SetPosition(const Vector2 &position) <Window::SetPosition>`
* :cpp:func:`ActivateConfiguration(WindowConfiguration *configuration, Mask mas) <Window::ActivateConfiguration>`

Mouse cursor
------------

* :cpp:func:`ShowCursor() <Window::ShowCursor>`
* :cpp:func:`HideCursor() <Window::HideCursor>`
* :cpp:func:`CaptureMouse() <Window::CaptureMouse>`
* :cpp:func:`ReleaseMouse() <Window::ReleaseMouse>`

Accessors
---------

* :cpp:func:`GetActiveScreen() const <Window::GetActiveScreen>`
* :cpp:func:`GetMainScreen() const <Window::GetMainScreen>`
* :cpp:func:`GetScreens() const <Window::GetScreens>`
* :cpp:func:`GetActiveConfiguration() const <Window::GetActiveConfiguration>`

Instance Methods
================

.. class:: Window
	
	.. function:: void SetTitle(const std::string &title)

		Sets the title of the window. By default this is the same as the application title.

	.. function:: void SetPosition(const Vector2 &position)

		Sets the position of the window relative to the top-left point of the active configurations screen.

	.. function:: void ActivateConfiguration(WindowConfiguration *configuration, Mask mask)

		Changes the currently active configuration of the window. This allows moving the window to another screen, changing its size and putting it into fullscreen mode etc.

	.. function:: void ShowCursor()

		Enables the hardware cursor (default)

	.. function:: void HideCursor()

		Disables the hardware cursor

	.. function:: void CaptureMouse()

		Captures the mouse within the client area of the rendering window.

	.. function:: void ReleaseMouse()

		Releases the mouse after it was previously captured within the client area of the rendering window.

	.. function:: Screen *GetActiveScreen() const

		Returns the currently active screen, that is, the screen the Rayne window was activated on.

	.. function:: Screen *GetMainScreen() const

		Returns the main screen. This is the same screen the Rayne window is initially opened on on startup.

	.. function:: std::vector<Screen *> &GetScreens() const

		Returns a vector of all screens currently attached to the computer.

	.. function:: WindowConfiguration *GetActiveConfiguration() const

		Returns the currently active configuration

Constants
=========

.. class:: Window

	.. type:: Mask
		
		* :code:`Fullscreen` The window will be displayed stretching over the full screen. The borderless mask is implied
		* :code:`Borderless` The window will be displayed without any border or drop shadow
		* :code:`VSync` Enables vertical sync on every v blank
