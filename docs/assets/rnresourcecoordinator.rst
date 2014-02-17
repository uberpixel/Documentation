.. _rnresourcecoordinator.rst:

***********************************
ResourceCoordinator class reference
***********************************

.. namespace:: RN
.. class:: ResourceCoordinator

+-------------------+-------------------------------------------------------------+
| **Inherits from** | :cpp:class:`ISingleton\<ResourceCoordinator\> <ISingleton>` |
+-------------------+-------------------------------------------------------------+
| **Availability**  | Rayne 1.0                                                   |
+-------------------+-------------------------------------------------------------+
| **Declared in**   | RNResourceCoordinator.h                                     |
+-------------------+-------------------------------------------------------------+

Overview
========

The resource coordinator is responsible for handling resource requests and dispatching them to the right :cpp:class:`ResourceLoader`, as well as caching already loaded resources and providing the user with the ability to alias them. It supports loading of resources both on the calling thread and also in a background thread via the use of futures and promises. By default, Rayne comes with resource loaders for `png`, `sgm` and shader files, but it can be extended to support other file types via custom :cpp:class:`ResourceLoader` subclasses.

Tasks
=====

Working with resources
----------------------

* :cpp:func:`GetResourceWithName(String *name, Dictionary *settings) <ResourceCoordinator::GetResourceWithName>`
* :cpp:func:`GetFutureResourceWithName(String *name, Dictionary *settings) <ResourceCoordinator::GetFutureResourceWithName>`
* :cpp:func:`AddResource(Object *resource, String *name) <ResourceCoordinator::AddResource>`
* :cpp:func:`AddResourceAlias(Object *resource, String *alias) <ResourceCoordinator::AddResourceAlias>`
* :cpp:func:`RemoveResource(Object *resource) <ResourceCoordinator::RemoveResource>`
* :cpp:func:`RemoveResourceWithName(String *name) <ResourceCoordinator::RemoveResourceWithName>`
* :cpp:func:`WaitForResources() <ResourceCoordinator::WaitForResources>`


Working with resource loaders
-----------------------------

* :cpp:func:`RegisterResourceLoader(ResourceLoader *loader) <ResourceCoordinator::RegisterResourceLoader>`
* :cpp:func:`UnregisterResourceLoader(ResourceLoader *loader) <ResourceCoordinator::UnregisterResourceLoader>`


Instance Methods
================

.. class:: ResourceCoordinator
	
	.. function:: T *GetResourceWithName(String *name, Dictionary *settings)

		Attempts to load the resource matching the given name, or serving it from the resource cache. The name must be either an alias to an already loaded resource, or a full qualified name/path which can be used by any of the resource loaders registered. The settings parameter is an optional parameter which can be used to pass additional settings to the resource loader.

		The full signature for the method is:

		.. code:: cpp

			template<class T>
			T *GetResourceWithName(String *name, Dictionary *settings)

		.. admonition:: Example

			.. code:: cpp

				RN::ResourceCoordinator *coordinator = RN::ResourceCoordinator::GetSharedInstance();
				RN::Texture *texture = coordinator->GetResourceWithName<RN::Texture>(RNCSTR("myTexture.png"), nullptr);

	.. function:: std::shared_future<Object *> GetFutureResourceWithName(String *name, Dictionary *settings)

		Attempts to load the resource matching the given name, or serving it from the resource cache. If the resource isn't loaded yet, it will be loaded in a background thread at a later point and the function will return immediately. You can use the returned future to access the loaded resource at a later point in time.

		The full signature for the method is:

		.. code:: cpp

			template<class T>
			std::shared_future<Object *> GetFutureResourceWithName(String *name, Dictionary *settings)

	.. function:: void AddResource(Object *resource, String *name)

		Manually adds the given resource to the resource coordinators cache. The resource will be retained by the resource coordinator and kept around until memory pressure arises, or the resource is removed manually later on. The name must be unique and not in use yet.

	.. function:: void AddResourceAlias(Object *resource, String *alias)

		Adds an alias to the given resource. The resource must already be in the resource cache, and the alias must be unique and not in use yet.

	.. function:: void RemoveResource(Object *resource)

		Removes the resource from the resource cache. This invalidates the resources name and any alias that may reference to it.

	.. function:: void RemoveResourceWithName(String *name)

		Removes the resource from the resource cache. The name can either be the original name used to load the resource, or one of its aliases.

	.. function:: void WaitForResources()

		Waits for all pending resource requests to complete.

	.. function:: void RegisterResourceLoader(ResourceLoader *loader)

		Registers the resource loader with the resource coordinator.

	.. function:: void UnregisterResourceLoader(ResourceLoader *loader)

		Removes a previously registered resource loader.
