.. _ralaudio_listener.rst

*****************************
AudioListener class reference
*****************************

.. namespace:: RN
.. namespace:: openal
.. class:: AudioListener

+-------------------+----------------------------------+
| **Inherits from** | :cpp:class:`SceneNodeAttachment` |
+-------------------+----------------------------------+
| **Availability**  | rayne-openal                     |
+-------------------+----------------------------------+
| **Declared in**   | RALAudioListener.h               |
+-------------------+----------------------------------+
| **Namespace**     | openal                           |
+-------------------+----------------------------------+

Overview
========

This class represents a point in the world that can hear audio, and relay it to the player's speakers.

Tasks
=====

* :cpp:func:`AudioListener() <AudioListener::AudioListener>`
* :cpp:func:`~AudioListener() override <AudioListener::~AudioListener>`	
* :cpp:func:`Update() <AudioListener::Update>`

Instance Methods
================

.. class:: AudioListener

	.. function:: AudioListener()
	
		Default constructor.

	.. function:: ~AudioListener() override
			
		Default destructor.

	.. function:: void Update(float delta)

		Call on update.