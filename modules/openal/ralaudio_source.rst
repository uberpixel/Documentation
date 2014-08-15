.. _ralaudio_listener.rst

***************************
AudioSource class reference
***************************

.. namespace:: RN
.. namespace:: openal
.. class:: AudioSource

+-------------------+------------------------+
| **Inherits from** | :cpp:class:`SceneNode` |
+-------------------+------------------------+
| **Availability**  | rayne-openal           |
+-------------------+------------------------+
| **Declared in**   | RALAudioSource.h       |
+-------------------+------------------------+
| **Namespace**     | openal                 |
+-------------------+------------------------+

Overview
========

This class represents objects that manage the playing of audio. It controls a bunch of sound properties, such as looping, and gives you an easy way to play them.

Tasks
=====

Construction and Destruction
----------------------------

* :cpp:func:`AudioSource() <AudioSource::AudioSource>`
* :cpp:func:`~AudioSource() override <AudioSource::~AudioSource>`

Actions
-------

* :cpp:func:`Update() override <AudioSource::Update>`
* :cpp:func:`Play() <AudioSource::Play>`

Setters
-------

* :cpp:func:`SetRepeat() <AudioSource::SetRepeat>`
* :cpp:func:`SetPitch() <AudioSource::SetPitch>`
* :cpp:func:`SetGain() <AudioSource::SetGain>`
* :cpp:func:`SetRange() <AudioSource::SetRange>`
* :cpp:func:`SetSelfdestruct() <AudioSource::SetSelfdestruct>`

Instance Methods
================

.. class:: AudioSource

	.. function:: AudioSource(AudioResource *asset)

		Default constructor. Takes a resource to wrap over.

	.. function:: ~AudioSource() override
			
		Default destructor.

	.. function:: void Update(float delta) override

		Call to take action on song completion for looping/self-destruction.

	.. function:: void Play()

		Play the sound.

	.. function:: void SetRepeat(bool repeat)

		Set whether the sound will repeat upon completion.

	.. function:: void SetPitch(float pitch)

		Set the pitch modulation on the sound. This makes the sound either higher or lower.

	.. function:: void SetGain(float gain)

		Set the gain modulation on the sound. This is the strength of the sound, which is sort of like volume but also isn't.

	.. function:: void SetRange(float min, float max)

		Set the range from which the sound can be heard.

	.. function:: void SetSelfdestruct(bool selfdestruct)

		Set whether the audio removes itself from the world upon completion.
