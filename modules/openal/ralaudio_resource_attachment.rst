.. _ralaudio_listener.rst

***************************************
AudioResourceAttachment class reference
***************************************

.. namespace:: RN
.. namespace:: openal
.. class:: AudioResourceAttachment

+-------------------+------------------------------+
| **Inherits from** | :cpp:class:`Object`          |
+-------------------+------------------------------+
| **Availability**  | rayne-openal                 |
+-------------------+------------------------------+
| **Declared in**   | RALAudioResourceAttachment.h |
+-------------------+------------------------------+
| **Namespace**     | openal                       |
+-------------------+------------------------------+

Overview
========

TBA

Tasks
=====

Construction and Destruction
----------------------------

* :cpp:func:`AudioResourceAttachment() <AudioResourceAttachment::AudioResourceAttachment>`
* :cpp:func:`~AudioResourceAttachment() <AudioResourceAttachment::~AudioResourceAttachment>`

Getters
-------

* :cpp:func:`GetBufferID() const <AudioResourceAttachment::GetBufferID>`
* :cpp:func:`GetAttachmentForResource() static <AudioResourceAttachment::GetAttachmentForResource>`

Class Methods
=============

.. class:: AudioResourceAttachment

	.. function:: static AudioResourceAttachment *GetAttachmentForResource(RN::AudioResource *resource)

Instance Methods
================

.. class:: AudioResourceAttachment

	.. function:: AudioResourceAttachment(RN::AudioResource *resource)

		Default constructor.

	.. function:: ~AudioResourceAttachment()

		Default destructor.

	.. function:: uint32 GetBufferID() const
			
