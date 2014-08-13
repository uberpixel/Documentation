.. _ralaudio_listener.rst

**************************
AudioWorld class reference
**************************

.. namespace:: RN
.. namespace:: openal
.. class:: AudioWorld

+-------------------+---------------------------------------------------------------------------------------+
| **Inherits from** | :cpp:class:`WorldAttachment`                                                          |
+-------------------+---------------------------------------------------------------------------------------+
|                   | :cpp:class:`INonConstructingSingleton\<AudioWorld\> <INonConstructingSingleton\<T\>>` |
+-------------------+---------------------------------------------------------------------------------------+
| **Availability**  | rayne-openal                                                                          |
+-------------------+---------------------------------------------------------------------------------------+
| **Declared in**   | RALAudioWorld.h                                                                       |
+-------------------+---------------------------------------------------------------------------------------+
| **Namespace**     | openal                                                                                |
+-------------------+---------------------------------------------------------------------------------------+

Overview
========

This class extends the default world, and provides advanced audio playing capabilities.

Tasks
=====

Construction and Destruction
----------------------------

* :cpp:func:`AudioWorld() <AudioWorld::AudioWorld>`
* :cpp:func:`~AudioWorld() override <AudioWorld::~AudioWorld>`

Actions
-------

* :cpp:func:`StepWorld() override <AudioWorld::StepWorld>`
* :cpp:func:`SetAudioListener() <AudioWorld::SetAudioListener>`
* :cpp:func:`PlaySound() <AudioWorld::PlaySound>`

Instance Methods
================

.. class:: AudioWorld

	.. function:: AudioWorld()
	
		Default constructor.

	.. function:: ~AudioWorld() override
			
		Default destructor.

	.. function:: void StepWorld(float delta) override
	
		Update the audio world for the time passed.

	.. function:: void SetAudioListener(AudioListener *attachment)
			
		Set the active listener that plays the sounds it receives.

	.. function:: AudioSource *PlaySound(AudioResource *resource)

		Play a sound.
