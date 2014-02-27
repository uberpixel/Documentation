.. _rnlightmanager.rst:

****************************
LightManager class reference
****************************

.. namespace:: RN
.. class:: LightManager

+-------------------+---------------------------+
| **Inherits from** | :cpp:class:`LightManager` |
+-------------------+---------------------------+
| **Availability**  | Rayne 1.0                 |
+-------------------+---------------------------+
| **Declared in**   | RNLightManager.h          |
+-------------------+---------------------------+

Overview
========

The LightManager class provides the interface definition for the way the renderer interacts with lights. It's responsible for preparing the light data it receives from the scene manager and make it available for shader usage. By default, Rayne uses a clustered light manager implemented in the :cpp:class:`ClusteredLightManager` class, however, you can create your own light managers by subclassing this class. A light manager is a per :cpp:class:`camera <Camera>` object, meaning that different cameras can use different light managers for their rendering.

Life cycle
----------

The light manager will receive any number of lights from the scene manager via the :cpp:func:`AddLight() <LightManager::AddLight>` method. Once the scene is build completely, the light manager will be asked to generate the light list data required for rendering via :cpp:func:`CreateLightLists() <LightManager::CreateLightLists>`, this may include further culling of the lights, creating light tiles or clusters, or any other required pre-processing step. When rendering, the light manager may be repeatedly ask to update shader data and adjust shader lookups to aid the renderer in finding and activating the right shader. Finally, at the end of the frame, the light manager will receive a :cpp:func:`ClearLights() <LightManager::ClearLights>` call, afterwards it may discard any data it doesn't need any more. This process is repeated for every frame in which the light manager is used.

Tasks
=====

Lights and light lists
----------------------

* :cpp:func:`virtual AddLight(Light *light) = 0 <LightManager::AddLight>`
* :cpp:func:`virtual CreateLightLists() = 0 <LightManager::CreateLightLists>`
* :cpp:func:`virtual ClearLights() = 0 <LightManager::ClearLights>`

Shader updates
--------------

* :cpp:func:`virtual UpdateProgram(Renderer *renderer, ShaderProgram *program) = 0 <LightManager::UpdateProgram>`
* :cpp:func:`virtual AdjustShaderLookup(Shader *shader, ShaderLookup &lookup) = 0 <LightManager::AdjustShaderLookup>`


Properties
----------

* :cpp:func:`virtual GetSpotLightCount() = 0 <LightManager::GetSpotLightCount>`
* :cpp:func:`virtual GetPointLightCount() = 0 <LightManager::GetPointLightCount>`
* :cpp:func:`virtual GetDirectionalLightCount() = 0 <LightManager::GetDirectionalLightCount>`
* :cpp:func:`GetCamera() const <LightManager::GetCamera>`


Instance Methods
================

.. class:: LightManager
	
	.. function:: void AddLight(Light *light)

		Called by the scene manager requesting to add the light to the light manager. Lights can be discarded, however, it's probably a better idea to first wait for all lights to be added before deciding which to discard.

	.. function:: void CreateLightLists()

		Invoked after all lights have been added. This is the point where subclasses should do any processing on the lights they received and preprare all data for later usage in the shaders (eg. update OpenGL buffers with the right data etc).

		.. note:: This method is called on the OpenGL queue

	.. function:: void ClearLights()

		Invoked after the renderer finished rendering using the light manager. At this point subclasses may discard any data they no longer need anymore.

	.. function:: void UpdateProgram(Renderer *renderer, ShaderProgram *program)

		Subclasses should use this to method to send all required data to the given shader program.

		.. note:: This method is called on the OpenGL queue

	.. function:: void AdjustShaderLookup(Shader *shader, ShaderLookup &lookup)

		Invoked by the renderer to finalize the shader lookup. Subclasses should look at the supported features of the shader and then decide which of them to activate for the shader lookup. Mutating the shader lookup in a way that it becomes invalid results in undefined behaviour.

		.. note:: This method is called on the OpenGL queue

	.. function:: size_t GetSpotLightCount()

		Subclasses must return the number of spot lights. This number doesn't have to be the same as the number of spot lights that have been added via :cpp:func:`AddLight <LightManager::AddLight>`, but it must be the number of lights that the light manager manages for this frame.

	.. function:: size_t GetPointLightCount()

		Subclasses must return the number of point lights. This number doesn't have to be the same as the number of point lights that have been added via :cpp:func:`AddLight <LightManager::AddLight>`, but it must be the number of lights that the light manager manages for this frame.

	.. function:: size_t GetDirectionalLightCount()

		Subclasses must return the number of directional lights. This number doesn't have to be the same as the number of directional lights that have been added via :cpp:func:`AddLight <LightManager::AddLight>`, but it must be the number of lights that the light manager manages for this frame.

	.. function:: Camera *GetCamera() const

		Returns the camera the light manager is attached to, or nullptr.
