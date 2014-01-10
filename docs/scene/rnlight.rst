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

Lights represent a light source within a scene. A light source lights up its immediate environment, and can optionally also cast shadows into the scene. There a three types of lights, Point lights, Spot lights and Directional lights. Every light has a colour and intensity, and additionally may also have a range and angle depending on the light type.

Tasks
=====

Construction
------------

* :cpp:func:`Light(Type type) <Light::Light>`

Shadows
-------

* :cpp:func:`ActivateShaodws(const ShadowParameter& parameter) <Light::ActivateShadows>`
* :cpp:func:`DeactivateShadows() <Light::DeactivateShadows>`
* :cpp:func:`HasShadows() const <Light::HasShadows>`
 

Instance Methods
================

.. class:: Light

	.. function:: Light(Type type = Type::PointLight)

		The designated constructor. Initializes the lights type to the given `type` parameter.

	.. function:: bool ActivateShadows(const ShadowParameter& parameter)

		Makes the light cast shadows.
		
Constants
=========

.. class:: Light 

	.. type:: Type
		
		* :code:`PointLight` Point light type.
		* :code:`SpotLight` Spot light type
		* :code:`DirectionalLight` Directional light type
