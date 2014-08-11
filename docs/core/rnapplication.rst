.. _rnapplication.rst:

***************************
Application class reference
***************************

.. namespace:: RN
.. class:: Application

+-------------------+------------------------------------------------------------------------------------------------------------------------------------+
| **Inherits from** | :cpp:class:`UI::Responder <UI::Responder>`, :cpp:class:`INonConstructingSingleton\<Application\> <INonConstructingSingleton\<T\>>` |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------+
| **Availability**  | Rayne 1.0                                                                                                                          |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------+
| **Declared in**   | RNApplication.h                                                                                                                    |
+-------------------+------------------------------------------------------------------------------------------------------------------------------------+

Overview
========

Root class that is used by the engine to communicate events back to the application. Every application needs its own sublcass of the Application class, which needs to be passed to the :cpp:class:`Kernel` class' constructor. Though it's not mandatory to override any of the methods, you usually want to provide implementations for the `Start` and `WillExit` methods to allow for proper construction and tear down of the engine.

.. note::
	
	The first time you can start interacting with Rayne is when the `Start` method of the Application is invoked. Before that, Rayne is in an inconsistent state and all but a few methods may have severe side effects. Methods guaranteed to work are:

	* :c:func:`RN::Initialize(int argc, char *argv[]) <Initialize>`
	* :cpp:func:`FileManager::AddSearchPath(const std::string &path) <FileManager::AddSearchPath>`
	* :cpp:func:`FileManager::GetSharedInstance() <FileManager::GetSharedInstance>`

Tasks
=====

Event handling
--------------

* :cpp:func:`virtual Start() <Application::Start>`
* :cpp:func:`virtual WillExit() <Application::WillExit>`
* :cpp:func:`virtual WillBecomeActive() <Application::WillBecomeActive>`
* :cpp:func:`virtual DidBecomeActive() <Application::DidBecomeActive>`
* :cpp:func:`virtual WillResignActive() <Application::WillResignActive>`
* :cpp:func:`virtual DidResignActive() <Application::DidResignActive>`
* :cpp:func:`virtual GameUpdate(float delta) <Application::GameUpdate>`
* :cpp:func:`virtual WorldUpdate(float delta) <Application::WorldUpdate>`

Misc
----

* :cpp:func:`SetTitle(const std::string &title) <Application::SetTitle>`
* :cpp:func:`GetTitle() const <Application::GetTitle>`


Instance Methods
================

.. class:: Application
	
	.. function:: void Start()

		Invoked when the kernel finished bootstrapping the engine, and all engine calls became available. At this point, the Kernel bootstrapped the basic input interface, the renderer as well as the rendering surface, amongst other things.

	.. function:: void WillExit()

		Called before the kernel will exit and tear down the engine. You should use this method to properly close any file handles, flush logs and do other kinds of clean ups required for a clean shut down.

	.. function:: void GameUpdate(float delta)

		Called every frame

	.. function:: void WorldUpdate(float delta)

		Called after each world step, ie once per frame if there is a completely loaded world available.

	.. function:: void WillBecomeActive()

		Called when the engine window is about to become active.

	.. function:: void DidBecomeActive()

		Called when the engine window became active

	.. function:: void WillResignActive()

		Called when the engine window is about to become inactive. Can be used to reduce the rendering FPS while the engine is in the background.

	.. function:: void DidResignActive()

		Called when the engine window did become inactive.

	.. function:: void SetTitle(const std::string &title)

		Changes the title displayed in the engine window

	.. function:: std::string &GetTitle() const

		Returns the title displayed in the engine window. This defaults to the application title as defined in the manifest.json
