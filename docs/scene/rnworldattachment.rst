.. _rnworldattachment.rst:

*******************************
WorldAttachment class reference
*******************************

.. namespace:: RN
.. class:: WorldAttachment

+---------------------+--------------------------------------+
|  **Inherits from**  | :cpp:class:`Object`                  |
+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNWorldAttachment.h                  |
+---------------------+--------------------------------------+

Overview
========

While the :cpp:class:`World` class represents a unique world, a world attachment represents a common interface that can be added to a world. An example for a world attachment would be a physics world attachment, which can be added to a world and drive the physics in there. World attachments get notified when the world they are attached to is changing, or when something within the world is changed.

Tasks
=====

Scene node changes
------------------

* :cpp:func:`virtual DidAddSceneNode(SceneNode *node) <WorldAttachment::DidAddSceneNode>`
* :cpp:func:`virtual WillRemoveSceneNode(SceneNode *node) <WorldAttachment::WillRemoveSceneNode>`
* :cpp:func:`virtual WillRenderSceneNode(SceneNode *node) <WorldAttachment::WillRenderSceneNode>`
* :cpp:func:`virtual SceneNodeDidUpdate(SceneNode *node, SceneNode::ChangeSet changeSet) <WorldAttachment::SceneNodeDidUpdate>`

Update events
-------------

* :cpp:func:`virtual StepWorld(float delta) <WorldAttachment::StepWorld>`
* :cpp:func:`virtual DidBeginCamera(Camera *camera) <WorldAttachment::DidBeginCamera>`
* :cpp:func:`virtual WillFinishCamera(Camera *camera) <WorldAttachment::WillFinishCamera>`


Instance Methods
================

.. class:: WorldAttachment
	
	.. function:: void StepWorld(float delta)

		Called once per frame when the scene nodes finished updating, but before they are rendered

	.. function:: void DidBeginCamera(Camera *camera)

		Called when the camera was selected for rendering, but before any scene node is passed to the rendered

	.. function:: void WillFinishCamera(Camera *camera)

		Called when the camera finished rendering

	.. function:: void DidAddSceneNode(SceneNode *node)

		Called when a scene node is added to the scene

	.. function:: void WillRemoveSceneNode(SceneNode *node)

		Called when a scene node is removed from the scene

	.. function:: void WillRenderSceneNode(SceneNode *node)

		Called when the scene node is about to get passed to the renderer

	.. function:: void SceneNodeDidUpdate(SceneNode *node, SceneNode::ChangeSet changeSet)

		Called when the scene node did change. You can examine the change set to find out about the kind of change that happened, eg. to identify wether the scene node was moved or if one of its children changed.
