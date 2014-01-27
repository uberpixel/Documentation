.. _rnlight.rst:

*********************
Light class reference
*********************

.. namespace:: RN
.. class:: Light 

+---------------------+--------------------------------------+
|  **Inherits from**  | :cpp:class:`SceneNode`               |
+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNLight.h                            |
+---------------------+--------------------------------------+

Overview
========

Lights represent light sources within a scene. A light source lights up its immediate environment, and can optionally also cast shadows into the scene. There are three types of lights: point lights, spot lights and directional lights. Every light has a color and intensity and additionally may also have a range and angle depending on the light type.

Shadows
-------

If shadows are activated, omni directional shadow mapping using cube maps will be used for point and spot lights. Parallel split shadow maps will be used for directional lights. There can only be one directional light casting shadows at a time. Also there can only be four shadow casting point lights and four shadow casting spot lights at a time.

Tasks
=====

Construction
------------

* :cpp:func:`Light(Type type) <Light::Light>`

Light parameters
----------------

* :cpp:func:`SetRange(float range) <Light::SetRange>`
* :cpp:func:`SetIntensity(float intensity) <Light::SetIntensity>`
* :cpp:func:`SetColor(const Color& color) <Light::SetColor>`
* :cpp:func:`SetAngle(float angle) <Light::SetAngle>`
* :cpp:func:`GetType() const <Light::GetType>`
* :cpp:func:`GetRange() const <Light::GetRange>`
* :cpp:func:`GetIntensity() const <Light::GetIntensity>`
* :cpp:func:`GetColor() const <Light::GetColor>`
* :cpp:func:`GetFinalColor() const <Light::GetFinalColor>`
* :cpp:func:`GetAngle() const <Light::GetAngle>`
* :cpp:func:`GetAngleCos() const <Light::GetAngleCos>`

Shadows
-------

* :cpp:func:`ActivateShadows(const ShadowParameter &parameter) <Light::ActivateShadows>`
* :cpp:func:`DeactivateShadows() <Light::DeactivateShadows>`
* :cpp:func:`SetSuppressShadows(bool suppress) <Light::SetSuppressShadows>`
* :cpp:func:`HasShadows() const <Light::HasShadows>`
* :cpp:func:`UpdateShadowParameters(const ShadowParameter &parameter) <Light::UpdateShadowParameters>`
* :cpp:func:`GetShadowParameters() const <Light::GetShadowParameters>`
* :cpp:func:`GetShadowMatrices() const <Light::GetShadowMatrices>`
* :cpp:func:`GetShadowDepthCameras() const <Light::GetShadowDepthCameras>`

Instance Methods
================

.. class:: Light

	.. function:: Light(Type type = Type::PointLight)

		The designated constructor. Initializes the lights type to the given `type` parameter.

	.. function:: void SetRange(float range)

		Sets the range of the light. The light will not effect anything outside this range. This only effects point and spot lights. The default range is 10.

	.. function:: void SetIntensity(float intensity)

		Sets the intensity of the light. This will make the light brighter without changing its range. Choosing a brighter color has the same effect.
		The default intensity is 10.

	.. function:: void SetColor(const Color& color)

		Sets the color of the light. The color will internally be scaled with the intensity.
		The default color is white.

	.. function:: void SetAngle(float angle)

		Sets the opening angle of spot lights. This does only effect spot lights.
		The default angle is 45 degrees.

	.. function:: Type GetType() const

		Returns the type of the light.

	.. function:: float GetRange() const

		Returns the lights range.

	.. function:: float GetIntensity() const

		Returns the lights intensity.

	.. function:: const Color& GetColor() const

		Returns the lights color.

	.. function:: const Vector3& GetFinalColor() const

		Returns the lights color multiplied with the intensity.

	.. function:: float GetAngle() const

		Returns the opening angle of a spot light.

	.. function:: float GetAngleCos() const

		Returns the cosine of a spot lights opening angle.

	.. function:: bool ActivateShadows(const ShadowParameter& parameter)

		Makes the light cast shadows. Returns true if shadows could successfully be activated, false otherwise.

		.. admonition:: Example

			.. code:: cpp

				// Create a directional light as sun
				RN::Light *sun = new RN::Light(RN::Light::Type:DirectionalLight);

				// Activate shadows for the main camera with default setup
				sun->ActivateShadows(RN::ShadowParameter(_camera));

	.. function:: void DeactivateShadows()

		Disables shadow casting and clears the whole shadow setup.

	.. function:: void SetSuppressShadows(bool suppress)

		Disables and enables shadow casting temporarily after shadows have already been activated and not deactivated. This is a better option than DeactivateShadows() if you only want to disable shadows for a short time. ActivateShadows() and DeactivateShadows() should usually be preferred.

	.. function:: void UpdateShadowParameters(const ShadowParameter& parameter)

		Allows to change the activated shadow setup. This will be slow for adding splits or changing the resolution but fast otherwise.

	.. function:: bool HasShadows()

		Returns true if the light is currently casting shadows. False otherwise.

	.. function:: ShadowParameter GetShadowParameters() const

		Returns the current shadow parameters.

	.. function:: const std::vector<Matrix>& GetShadowMatrices() const

		Returns the matrices used for the current frames shadow projection. Will be empty if shadows are not activated.

	.. function:: Array* GetShadowDepthCameras() const

		Returns the cameras used for rendering the depth maps needed for the currently active shadows. Will be empty if shadows are not activated.

Structures
==========

ShadowSplit
-----------

.. class:: ShadowSplit

	This structure holds the settings for a single parallel split shadow map split or depth cube map. Directional shadows usually have around four of these while spot and point light shadows only use one.

	.. function:: ShadowSplit(size_t updateInterval=1, size_t updateOffset=0)

		Initializes the structure with the given parameters.

	.. member:: float biasFactor = 2.0

		The polygon offset factor used for the shadow mapping to reduce shadow acne.

	.. member:: float biasFactor = 512.0

		The polygon offset unit used for the shadow mapping to reduce shadow acne.

	.. member:: size_t updateInterval = 1

		This is the interval in frames in which the shadow split is updated. The default value of 1 will update it every frame, while a value of 4 would only update every four frames.

	.. member:: size_t updateOffset = 0

		This an offset in frames used to shift the time of updating the split within the set updateInterval. This allows for example to have four splits each updated every four frames but all in a different frames. This can be used to reduce the work that has to be done within a single frame.

ShadowParameter
---------------

.. class:: ShadowParameter

	This structure holds the settings used for shadows. Directional shadows do need to have the shadowTarget camera set to the camera, the shadows should be seen in.
	The default setup for directional shadows uses 4 splits with the first one updating every frame, the second and the third every 2 frames and the fourth only every three frames. This setup usually provides a good compromise of quality and speed, but with fast moving light or objects it can be desirable to update the splits every frame for a good appearance.

	.. function:: ShadowParameter(size_t resolution=1024)

		Initializes the structure with the given shadow map resolution and one split. This should be used for point and spot lights.

	.. function:: ShadowParameter(Camera *target, size_t resolution = 1024)

		Initializes the structure with the given shadowTarget camera and shadow map resolution. It also adds fours splits. This should be used for directional lights.

	.. member:: size_t resolution = 1024

		The depth map resolution used for the shadows. This value should be a power of two, a higher value will produce sharper shadows and should usually not be bigger than 4096.

	.. member:: std::vector<ShadowSplit> splits

		The shadow splits containing bias and update information for each split or cube map.

	.. member:: float distanceBlendFactor = 0.05f

		This factor between 0 and 1 is used for directional shadows to blend determine the distances for each split. A higher value will make the closer splits bigger and the ones further away smaller.
		Internally it is used to blend between logarithmic and linear split distances.

	.. member:: Camera *shadowTarget = nullptr

		This is only used for directional shadows and specifies the camera they are set up for. It cannot be nullptr for directional shadows!

Constants
=========

.. class:: Light 

	.. type:: Type
		
		* :code:`PointLight` Point light type.
		* :code:`SpotLight` Spot light type
		* :code:`DirectionalLight` Directional light type
