.. _rnkernel.rst:

**********************
Kernel class reference
**********************

.. namespace:: RN
.. class:: Kernel

+-------------------+------------------------------------------------------------------------------+
| **Inherits from** | :cpp:class:`INonConstructingSingleton\<Kernel\> <INonConstructingSingleton>` |
+-------------------+------------------------------------------------------------------------------+
| **Availability**  | Rayne 1.0                                                                    |
+-------------------+------------------------------------------------------------------------------+
| **Declared in**   | RNKernel.h                                                                   |
+-------------------+------------------------------------------------------------------------------+

Overview
========

The Kernel class implements the core book keeping class within Rayne. The kernel is responsible for bootstrapping the engine itself and keeping track of OS events, input, rendering, scenes and time, among others. It also drives the application itself, dispatching update events to the scene and initiating the rendering of the frame.

Before you can do anything useful with Rayne, you'll have to create an instance of this class and initialize it with the application itself. A typical application life cycle looks like this:

.. admonition:: Example
	
	.. code:: cpp

		int main(int argc, char *argv[])
		{
			RN::Initialize(argc, argv); // Initialize core routines and parse command line arguments

			try
			{
				MyApplication *application = new MyApplication(); // Create a new application instance
				RN::Kernel *kernel = new RN::Kernel(application); // Create the kernel that drives the game
				
				while(kernel->Tick()) // Render frames
				{}
				
				// Clean up
				delete kernel;
				delete application;
			}
			catch(RN::Exception e)
			{
				RN::HandleException(e); // Error handling
				return EXIT_FAILURE;
			}
			
			return EXIT_SUCCESS;
		}


Tasks
=====

Construction
------------

* :cpp:func:`Kernel(Application *app) <Kernel::Kernel>`

Application life cycle
----------------------

* :cpp:func:`Tick() <Kernel::Tick>`
* :cpp:func:`DidSleepForSignificantTime() <Kernel::DidSleepForSignificantTime>`
* :cpp:func:`Exit() <Kernel::Exit>`
* :cpp:func:`GetTitle() const <Kernel::GetTitle>`
* :cpp:func:`GetWindow() const <Kernel::GetWindow>`

Time
----

* :cpp:func:`SetFixedDelta(float delta) <Kernel::SetFixedDelta>`
* :cpp:func:`SetTimeScale(double scale) <Kernel::SetTimeScale>`
* :cpp:func:`SetMaxFPS(uint32 fps) <Kernel::SetMaxFPS>`
* :cpp:func:`GetDelta() const <Kernel::GetDelta>`
* :cpp:func:`GetTimeScale() const <Kernel::GetTimeScale>`
* :cpp:func:`GetTime() const <Kernel::GetTime>`
* :cpp:func:`GetScaledTime() const <Kernel::GetScaledTime>`
* :cpp:func:`GetCurrentFrame() const <Kernel::GetCurrentFrame>`
 

High resolution rendering
-------------------------

* :cpp:func:`GetScaleFactor() const <Kernel::GetScaleFactor>`
* :cpp:func:`GetActiveScaleFactor() const <Kernel::GetActiveScaleFactor>`

Statistics
----------

* :cpp:func:`PushStatistics(const std::string &key) <Kernel::PushStatistics>`
* :cpp:func:`PopStatistics() <Kernel::PopStatistics>`
* :cpp:func:`GetStatisticsData() const <Kernel::GetStatisticsData>`

Windows only
------------

* :cpp:func:`GetMainWindow() const <Kernel::GetMainWindow>`
* :cpp:func:`GetInstance() const <Kernel::GetInstance>`


Instance Methods
================

.. class:: Kernel
	
	.. function:: Kernel(Application *app)

		Constructor for the kernel. Must be passed a valid :cpp:class:`Application` subclass, representing the application. Before this call, most Rayne methods and classes won't work or do unexpected things, since the kernel is responsible for bootstrapping Rayne.

	.. function:: bool Tick()

		Advances the engines state by one frame. This method is responsible for listening to OS events, dispatching the input, updating the world and ultimately rendering it. This method will return true if more frames can be rendered, otherwise it will return false and it shouldn't be invoked afterwards again.

	.. function:: void Exit()

		Marks the engine for exit. `Tick` will return false the next time it completes.

	.. function:: void DidSleepForSignificantTime()

		Should be invoked after the app spend a long time without any `Tick` to avoid sudden jolts in the framerate and movement. This method is rarely useful beyond mobile where apps can be put in a frozen state for an indefinite amount of time.

	.. function:: const std::string &GetTitle() const

		Returns the application title as it's found in the manifest.json

	.. function:: Window *GetWindow() const

		Returns the window that Rayne is currently rendering into

	.. function:: void SetFixedDelta(float delta)

		Fixes the delta to the given amount. No matter how long a frame will take to complete, it will seem like it took exactly `delta` time. This is useful when trying to record video at a fixed frame rate. Setting this to 0.0 (default) turns off rendering with a fixed time delta.

	.. function:: void SetTimeScale(double scale)

		Sets the factor by which time should be scaled (defaults to 1.0). Can be used to implement bullet time effects and similar.

	.. function:: void SetMaxFPS(uint32 fps)

		Sets the maximum FPS (default 120). This method can be used to save power to not render more frames than actually needed.

	.. function:: float GetDelta() const

		Returns the time delta of the current frame

	.. function:: double GetTimeScale() const

		Returns the currently used time scale

	.. function:: double GetTime() const

		Returns the amount of time passed since the application start.

	.. function:: double GetScaledTime() const

		Returns the amount of time passed since the application start with respect to the time scale.

	.. function:: FrameID GetCurrentFrame() const

		Returns the ID of the current frame

	.. function:: float GetScaleFactor() const

		Returns the system scale factor for high resolution rendering. On high resolution displays, the returned variable is >= 1.0 and determines the scale factor between a hardware pixel and a point.

	.. function:: float GetActiveScaleFactor() const

		Returns the active scale factor for the current rendering device.

	.. function:: void PushStatistics(const std::string &key)

		Pushes the given statistics to the thread local statistics pool.

	.. function:: void PopStatistics()

		Pops the active statistics from the thread local statistics pool.

	.. function:: const std::vector<Statistics::DataPoint *> &GetStatisticsData() const

		Returns the statistics data gathered in the last frame.

	.. function:: HWND GetMainWindow() const

		Returns the main backing window used by the engine. This window isn't visible and not the rendering window, instead, the rendering window is attached to the main window as child.

	.. function:: HINSTANCE GetInstance() const

		Returns the HINSTANCE of the engine.

Messages
========

	The following messages are send out by the kernel:

	.. type:: kRNKernelDidBeginFrameMessage

		Send at the beginning of a frame, after dispatching input data and readying the renderer. The object and info dictionary are nullptr.

	.. type:: kRNKernelDidEndFrameMessage

		Send after the frame finished rendering, but before the front and back buffer are switched. The object and info dictionary are nullptr.

