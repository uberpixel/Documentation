.. _rnresourceloader.rst:

******************************
ResourceLoader class reference
******************************

.. namespace:: RN
.. class:: ResourceLoader

+-------------------+---------------------+
| **Inherits from** | :cpp:class:`Object` |
+-------------------+---------------------+
| **Availability**  | Rayne 1.0           |
+-------------------+---------------------+
| **Declared in**   | RNResourceLoader.h  |
+-------------------+---------------------+

Overview
========

The ResourceLoader class provides the interface required to add support for additional resource support. For example, you can provide a custom resource loader to load your own proprietary assets, or add support for an already existing asset format. ResourceLoaders are registered with the :cpp:class:`ResourceCoordinator`, which is responsible for picking the right resource loader for any requested asset.

There are two types of resource loader possible, the first one is the classical resource load which takes a physical file on disk and transforms it into a resource usable by Rayne, the second type takes a simple string argument and either uses that to generate the resource, or use it to look the resource up somewhere. Resource loaders that don't load real files are called imaginary file resource loader.

You usually want to register your resource loaders as soon as possible, in which case it makes sense to override the :cpp:func:`InitialWakeUp() <Object::InitialWakeUp>` method and use it to register the resource coordinator right away. 

.. admonition:: Example
	
	.. code:: cpp

		void MyResourceLoader::InitialWakeUp(RN::MetaClassBase *meta)
		{
			if(meta == MetaClass())
			{
				MyResourceLoader *loader = new MyResourceLoader();
				RN::ResourceCoordinator::GetSharedInstance()->RegisterResourceLoader(loader);
				loader->Release(); // The resource coordinator holds a reference to it
			}
		}

Tasks
=====

Constructor

* :cpp:func:`ResourceLoader(MetaClassBase *resourceClass) <ResourceLoader::ResourceLoader>`

Capability reporting
--------------------

* :cpp:func:`virtual SupportsBackgroundLoading() <ResourceLoader::SupportsBackgroundLoading>`
* :cpp:func:`virtual SupportsLoadingFile(File *file) <ResourceLoader::SupportsLoadingFile>`
* :cpp:func:`virtual SupportsLoadingName(String *name) <ResourceLoader::SupportsLoadingName>`
* :cpp:func:`virtual GetPriority() const <ResourceLoader::GetPriority>`
* :cpp:func:`GetResourceClass() const <ResourceLoader::GetResourceClass>`
* :cpp:func:`SetFileExtensions(const std::vector\<std::string\> &extensions) <ResourceLoader::SetFileExtensions>`
* :cpp:func:`SetMagicBytes(const Date *data, size_t begin) <ResourceLoader::SetMagicBytes>`
* :cpp:func:`SetSupportsImaginaryFiles(bool support) <ResourceLoader::SetSupportsImaginaryFiles>`

Resource loading
----------------

* :cpp:func:`virtual Load(File *file, Dictionary *settings) <ResourceLoader::Load>`
* :cpp:func:`virtual Load(String *name, Dictionary *settings) <ResourceLoader::Load>`

Instance Methods
================

.. class:: ResourceLoader
	
	.. function:: ResourceLoader(MetaClassBase *resourceClass)

		Designated constructor. The `resourceClass` must match the class type the resource loader is capable of loading, for example, a texture loader might pass `RN::Texture2D::MetaClass()` as parameter.

	.. function:: bool SupportsBackgroundLoading()

		If this function returns true (default), the resource loader may be called from multiple threads. You are encouraged to add background loading support when creating new resource loaders.

	.. function:: bool SupportsLoadingFile(File *file)

		If this function returns true (default), the resource loader is capable of loading the given file. This method is invoked after file extension and magic bytes have been matched, and can be used as a last sanity check to make sure loading the file is supported. In general, if you correctly set the magic bytes and file extension, there is rarely any use in overriding this function.

		.. note:: Only applicable to file based resource loaders!

	.. function:: bool SupportsLoadingName(String *name)

		This function is used to determine if the resource loader is capable of loading or creating a resource based on the given name. It is only invoked for imaginary file based resource loaders, and works analogous to the :cpp:func:`SupportsLoadingFile` method.

		.. note:: Only applicable to imaginary file based resource loaders!

	.. function:: int32 GetPriority() const

		Returns the priority of the resource loader (default 10). The priority is used to determine which resource loader to pick if multiple resource loader support loading a given file. The resource coordinator will pick the resource loader with the lowest priority to load a resource. The default priority for the built in Rayne resource loaders is 100.

	.. function:: MetaClassBase *GetResourceClass() const

		Returns the class the resource loader is capable of loading.

	.. function:: void SetFileExtensions(const std::vector<std::string> &extensions)

		Sets the file extensions supported by the receiver. This should usually be set at constructor time and then be left unchanged. The resource loader is only considered to be capable of loading a resource if the file extensions match the requested file. By default there is no file extension limitations.

		.. note:: Only applicable to file based resource loaders!

	.. function:: void SetMagicBytes(const Data *data, size_t begin)

		Sets the magic bytes that must be present starting at `begin` of the file. The resource loader is only considered capable of loading a resource if the magic bytes match with the ones found in the file. The default is to just accept any magic bytes.

		.. note:: Only applicable to file based resource loaders!

	.. function:: void SetSupportsImaginaryFiles(bool support)

		Enables or disables support for imaginary files (default false). This method should be called at constructor time and then be left unchanged.

	.. function:: Object *Load(File *file, Dictionary *settings)

		Subclasses must override this method to load the given file. The returned objects class must match the resource class given to the constructor. Any thrown exceptions are hoisted back to the requester of the resource.

		.. note:: Only applicable to file based resource loaders!

	.. function:: Object *Load(String *name, Dictionary *settings)

		Subclasses must override this method to load the given name. The returned objects class must match the resource class given to the constructor. Any thrown exceptions are hoisted back to the requester of the resource.

		.. note:: Only applicable to imaginry file based resource loaders!
