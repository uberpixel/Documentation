.. _rnbillboard.rst:

*************************
Billboard class reference
*************************

.. namespace:: RN
.. class:: Billboard 

+---------------------+--------------------------------------+
|  **Inherits from**  | :cpp:class:`SceneNode`               |
+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNBillboard.h                        |
+---------------------+--------------------------------------+

Overview
========

The Billboard class implements a 2D textured node within a scene. Unlike many other engines where billboards, or sprites, don't have an orientation, billboards in Rayne do have one and don't automatically face the camera.

Tasks
=====

Construction
------------

* :cpp:func:`Billboard() <Billboard::Billboard>`
* :cpp:func:`Billboard(Texture *texture) <Billboard::Billboard>`
* :cpp:func:`Billboard(Texture *texture, const Vector3 &position) <Billboard::Billboard>`

Appearance
----------

* :cpp:func:`SetTexture(Texture *texture, float scaleFactor = 0.1f) <Billboard::SetTexture>`
* :cpp:func:`GetMaterial() const <Billboard::GetMaterial>`
* :cpp:func:`GetTexture() const <Billboard::GetTexture>`
* :cpp:func:`GetSize() const <Billboard::GetSize>`

Instance Methods
================

.. class:: Billboard

	.. function:: Billboard()

		Initializes the billboard without a texture at position `0|0|0`

	.. function:: Billboard(Texture *texture)

		Initializes the billboard with the given texture at position `0|0|0`

	.. function:: Billboard(Texture *texture, const Vector3 &position)

		Initializes the billboard with the given texture and position

	.. function:: void SetTexture(Texture *texture, float scaleFactor = 0.1f)

		Sets the texture of the receiver and also its scale factor (default 0.1f). The scale factor is used to scale the billboard in world space to fit with the scaling system of your world. When set to `1.0f`, one pixel of the texture represents 1 unit of world space. The texture mustn't be NULL.

	.. function:: Material *GetMaterial() const

		Returns the material of the receiver. You are strongly discouraged from altering the shader, defines and textures of the returned material.

	.. function:: Texture *GetTexture() const

		Returns the currently set texture of the receiver or nullptr

	.. function:: const Vector2 &GetSize() const

		Returns the size of the receiver in world space.
		