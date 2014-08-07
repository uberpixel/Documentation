.. _raresource_loader_assimp.rst

************************************
AssimpResourceLoader class reference
************************************

.. namespace:: RN
.. namespace:: assimp
.. class:: AssimpResourceLoader

+-------------------+-----------------------------+
| **Inherits from** | :cpp:class:`ResourceLoader` |
+-------------------+-----------------------------+
| **Availability**  | rayne-assimp                |
+-------------------+-----------------------------+
| **Declared in**   | RAResourceLoaderAssimp.h    |
+-------------------+-----------------------------+
| **Namespace**     | assimp                      |
+-------------------+-----------------------------+

Overview
========

This class is a loader which greatly expands the number of 3D model types that can be loaded into Rayne. If you plan on having your game expandable and moddable, this is probably a good addition to have, because it reduces the number of hoops that modders have to jump through in order to add to your game. Otherwise, they have to convert all of their models to Rayne's format, which requires blender and a special plugin.

Tasks
=====

* :cpp:func:`AssimpResourceLoader() <AssimpResourceLoader::AssimpResourceLoader>`
* :cpp:func:`Load() override <AssimpResourceLoader::Load>`
* :cpp:func:`SupportsBackgroundLoading() override <AssimpResourceLoader::SupportsBackgroundLoading>`
* :cpp:func:`SupportsLoadingFile() override <AssimpResourceLoader::SupportsLoadingFile>`
* :cpp:func:`GetPriority() const override <AssimpResourceLoader::GetPriority>`
* :cpp:func:`InitialWakeUp() static <AssimpResourceLoader::InitialWakeUp>`

Class Methods
=============

.. class:: AssimpResourceLoader

	.. function:: static void InitialWakeUp(MetaClass *meta)

		Register the resource loader with Rayne. This should generally be done as soon as possible.

Instance Methods
================

.. class:: AssimpResourceLoader

	.. function:: AssimpResourceLoader()
			
		Default constructor.

	.. function:: Asset *Load(File *file, Dictionary *settings) override
			
		Load a model from a file.

	.. function:: bool SupportsBackgroundLoading() override

		Get if the loader supports background loading.

	.. function:: bool SupportsLoadingFile(File *file) override
			
		See if a specific file can be loaded with this loader.

	.. function:: uint32 GetPriority() const override

		This gets the priority set on the loader, which is a tie-breaker if there are multiple loaders for a single file. See :cpp:class:`ResourceLoader <ResourceLoader>` for more information.
