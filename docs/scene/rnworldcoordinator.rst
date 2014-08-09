.. _rnworldcoordinator.rst:

********************************
WorldCoordinator class reference
********************************

.. namespace:: RN
.. class:: WorldCoordinator

+-------------------+---------------------------------------------------------------+
| **Inherits from** | :cpp:class:`ISingleton\<WorldCoordinator\> <ISingleton\<T\>>` |
+-------------------+---------------------------------------------------------------+
| **Availability**  | Rayne 1.0                                                     |
+-------------------+---------------------------------------------------------------+
| **Declared in**   | RNWorldCoordinator.h                                          |
+-------------------+---------------------------------------------------------------+

Overview
========

The WorldCoordinator singleton provides means to load and save worlds. It also keeps track of the currently active world and handles its relationship with the :cpp:class:`Kernel`, and acts as event proxy between the two.

The WorldCoordinator class is also used to make a world active, by using the :cpp:func:`LoadWorld() <WorldCoordinator::LoadWorld>` function.

Tasks
=====

Loading worlds
--------------

* :cpp:func:`LoadWorld(World *world) <WorldCoordinator::LoadWorld>`
* :cpp:func:`LoadWorld(const std::string &file) <WorldCoordinator::LoadWorld>`
* :cpp:func:`LoadWorld(Deserialiter *deserializer) <WorldCoordinator::LoadWorld>`
* :cpp:func:`IsLoading() const <WorldCoordinator::IsLoading>`
  
Saving worlds
-------------

* :cpp:func:`SaveWorld(const std::string &file) <WorldCoordinator::SaveWorld>`
* :cpp:func:`SaveWorld(Serializer *serializer) <WorldCoordinator::SaveWorld>`

Misc
----

* :cpp:func:`GetWorld() const <WorldCoordinator::GetWorld>`
* :cpp:func:`GetWorldFile() const <WorldCoordinator::GetWorldFile>`


Instance Methods
================

.. class:: WorldCoordinator

	.. function:: Progress *LoadWorld(World *world)

		Attempts to load the given world. The return value is an async :cpp:class:`Progress` object that can be used to monitor the loading progress. If the given world doesn't support background loading, it will be loaded blocking on the calling thread and the world is finished loading upon return.

		.. note:: Only one world can be loaded at once, this method will throw an exception if there is a second loading attempt while an old one is still running
		.. note:: Upon return, the given world is already the active world.

	.. function:: Progress *LoadWorld(const std::string &file)

		Opens the file and loads it using the default deserializer class into a new world, which is then made active.

	.. function:: Progress *LoadWorld(Deserializer *deserializer)

		Loads a world that has been previously serialized from the given deserializer.

	.. function:: bool IsLoading() const

		Returns true if the world coordinator is currently loading a world

	.. function:: void SaveWorld(const std::string &file)

		Saves the active world into the specified file using the default serializer class.

	.. function:: void SaveWorld(Serializer *serializer)

		Saves the active world into the given serializer, but doesn't write it to disk.

	.. function:: World *GetWorld() const

		Returns the currently managed world.

	.. function:: std::string GetWorldFile() const

		If the world has been loaded from a file, the path of that file is returned by this function, otherwise an empty string.

Messages
========

.. type:: kRNWorldCoordinatorWillBeginLoadingMessage

	Send by the world coordinator when it starts loading a new world. The object is the world being loaded and the info dictionary is nullptr.

.. type:: kRNWorldCoordinatorDidFinishLoadingMessage

	Send by the world coordinator when it finishes loading a new world. The object is the world that has been loaded and the info dictionary is nullptr.

.. type:: kRNWorldCoordinatorDidStepWorldMessage

	Send by the world coordinator after updating the world but before rendering it. The object is the currently active world.


