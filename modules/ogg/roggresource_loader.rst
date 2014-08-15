.. _roggresource_loader.rst

************************************
OggResourceLoader class reference
************************************

.. namespace:: RN
.. namespace:: ogg
.. class:: OggResourceLoader

+-------------------+-----------------------------+
| **Inherits from** | :cpp:class:`ResourceLoader` |
+-------------------+-----------------------------+
| **Availability**  | rayne-ogg                   |
+-------------------+-----------------------------+
| **Declared in**   | ROGGResourceLoader.h        |
+-------------------+-----------------------------+
| **Namespace**     | ogg                         |
+-------------------+-----------------------------+

Overview
========

OGG files are commonly used to hold audio because they are standardized and do not have IP concerns. Thanks to this, there is a tiny public domain library called `stb_vorbis <https://github.com/nothings/stb>`_ that can import these easily, and that is what this loader is based off of.

Tasks
=====

* :cpp:func:`OggResourceLoader() <OggResourceLoader::OggResourceLoader>`
* :cpp:func:`Load() override <OggResourceLoader::Load>`
* :cpp:func:`SupportsBackgroundLoading() override <OggResourceLoader::SupportsBackgroundLoading>`
* :cpp:func:`SupportsLoadingFile() override <OggResourceLoader::SupportsLoadingFile>`
* :cpp:func:`GetPriority() const override <OggResourceLoader::GetPriority>`
* :cpp:func:`InitialWakeUp() static <OggResourceLoader::InitialWakeUp>`

Class Methods
=============

.. class:: OggResourceLoader

	.. function:: static void InitialWakeUp(MetaClass *meta)

		Register the resource loader with Rayne. This should generally be done as soon as possible.

Instance Methods
================

.. class:: OggResourceLoader

	.. function:: OggResourceLoader()
			
		Default constructor.

	.. function:: Asset *Load(File *file, Dictionary *settings) override
			
		Load a model from a file.

	.. function:: bool SupportsBackgroundLoading() override

		Get if the loader supports background loading.

	.. function:: bool SupportsLoadingFile(File *file) override
			
		See if a specific file can be loaded with this loader.

	.. function:: uint32 GetPriority() const override

		This gets the priority set on the loader, which is a tie-breaker if there are multiple loaders for a single file. See :cpp:class:`ResourceLoader <ResourceLoader>` for more information.
