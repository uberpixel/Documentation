.. _rnworldcoordinator.rst:

********************************
WorldCoordinator class reference
********************************

.. namespace:: RN
.. class:: WorldCoordinator

+---------------------+-----------------------------------------------------------+
|  **Inherits from**  | :cpp:class:`ISingleton\<WorldCoordinator\> <ISingleton>`  |
+---------------------+-----------------------------------------------------------+
|   **Availability**  | Rayne 1.0                                                 |
+---------------------+-----------------------------------------------------------+
| **Declared in**     | RNWorldCoordinator.h                                      |
+---------------------+-----------------------------------------------------------+

Overview
========

The WorldCoordinator singleton provides means to load and save worlds. It also keeps track of the currently active world and handles its relationship with the :cpp:class:`Kernel`, and acts as event proxy between the two.

The WorldCoordinator class is also used to make a world active, by using the :cpp:func:`LoadWorld() <WorldCoordinator::LoadWorld>` function.

Tasks
=====

Loading worlds
--------------

* :cpp:func:`LoadWorld(World *world) <WorldCoordinator::LoadWorld>`
* :cpp:func:`IsLoading() const <WorldCoordinator::IsLoading>`

Misc
----

* :cpp:func:`GetWorld() const <WorldCoordinator::GetWorld>`


Instance Methods
================

.. class:: WorldCoordinator

	.. function:: Progress *LoadWorld(World *world)

		Attempts to load the given world. The return value is an async :cpp:class:`Progress` object that can be used to monitor the loading progress. If the given world doesn't support background loading, it will be loaded blocking on the calling thread and the world is finished loading upon return.

		.. note:: Only one world can be loaded at once, this method will throw an exception if there is a second loading attempt while an old one is still running
		.. note:: Upon return, the given world is already the active world.

	.. function:: bool IsLoading() const

		Returns true if the world coordinator is currently loading a world

	.. function:: World *GetWorld() const

		Returns the currently managed world.