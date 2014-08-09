.. _rnworld.rst:

*********************
World class reference
*********************

.. namespace:: RN
.. class:: World 

+---------------------+--------------------------------------+
|  **Inherits from**  | :cpp:class:`Object`                  |
+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNWorld.h                            |
+---------------------+--------------------------------------+

Overview
========

The World class encapsulates a complete scene, and means to load and save it. It also provides mechanism to listen for changes within a scene, for example added or removed scene nodes, via the :cpp:class:`WorldAttachment` class. Lastly, together with a scene manager, it provides the means required to render a scene, by tracking all :cpp:class:`Camera` within it and rendering them via the scene manager.

Subclassing
-----------

While a World by itself already provides a number of useful implementations, it's usually a good idea to create one or more subclasses that take care of loading and/or saving of the world, or creating the world entirely through code. Even though these operations are common to all worlds, it's impossible to provide a common implementation for them. The World class allows you to define your own, custom and specialized level format that can then be loaded by a custom subclass, allowing a great deal of flexibility.

Most likely you'll want to subclass the :cpp:func:`LoadOnThread() <World::LoadOnThread>` and :cpp:func:`SupportsBackgroundLoading() <World::SupportsBackgroundLoading>` methods to define your loading and/or scene creation mechanism.

Scene nodes and the active world
--------------------------------

Newly created scene nodes are automatically added to the currently active world, so there is no need to do this manually. They can, however, be removed from their world and inserted into another, non-active one. Simply creating a World doesn't automatically make it the active one, it first has to be made active via the :cpp:class`WorldCoordinator` singleton, which is also the reason it's not encouraged to start creating or loading the World within its constructor. Instead, the :cpp:func:`LoadOnThread() <World::LoadOnThread>` method should be used for that.

Modes
-----

A world is in one of two modes, `Play` or `Edit`. By default a world will be in `Play` mode which is the default mode for running games. The edit mode is designed for real time editors like Downpour to allow the world to run different actions, for example in Edit mode, NPCs and physics should probably not be updated.

Tasks
=====

Construction
------------

* :cpp:func:`World(SceneManager *sceneManager) <World::World>`
* :cpp:func:`World(const std::string &sceneManager) <World::World>`

Driving the world
-----------------

* :cpp:func:`virtual Update(float delta) <World::Update>`
* :cpp:func:`virtual UpdateEditMode(float delta) <World::UpdateEditMode>`
* :cpp:func:`virtual DidUpdateToFrame(FrameID frame) <World::DidUpdateToFrame>`

Handling scene nodes
--------------------

* :cpp:func:`AddSceneNode(SceneNode *node) <World::AddSceneNode>`
* :cpp:func:`RemoveSceneNode(SceneNode *node) <World::RemoveSceneNode>`
* :cpp:func:`DropSceneNodes() <World::DropSceneNodes>`
* :cpp:func:`ApplyNodes() <World::ApplyNodes>`

Attachments
-----------

* :cpp:func:`AddAttachment(WorldAttachment *attachment) <World::AddAttachment>`
* :cpp:func:`RemoveAttachment(WorldAttachment *attachment) <World::RemoveAttachment>`

Loading and Saving
------------------

* :cpp:func:`virtual LoadOnThread(Thread *thread, Deserializer *deserializer) <World::LoadOnThread>`
* :cpp:func:`virtual FinishLoading(Deserializer *deserializer) <World::FinishLoading>`
* :cpp:func:`virtual SupportsBackgroundLoading() const <World::SupportsBackgroundLoading>`
* :cpp:func:`virtual SaveOnThread(Thread *thread, Serializer *serializer) <World::SaveOnThread>`
* :cpp:func:`virtual FinishSaving(Serializer *serializer) <World::FinishSaving>`
* :cpp:func:`virtual SupportsBackgroundSaving() const <World::SupportsBackgroundSaving>`

Accessing the scene tree
------------------------

* :cpp:func:`GetSceneManager() const <World::GetSceneManager>`
* :cpp:func:`GetSceneNodes() <World::GetSceneNodes>`
* :cpp:func:`GetSceneNodeWithTag(Tag tag) <World::GetSceneNodeWithTag>`
* :cpp:func:`GetSceneNodesWithTag(Tag tag) <World::GetSceneNodesWithTag>`

Working with Modes
------------------

* :cpp:func:`SetMode(Mode mode) <World::SetMode>`
* :cpp:func:`GetMode(Mode mode) <World::GetMode>`

Misc
----

* :cpp:func:`static GetActiveWorld() const <World::GetActiveWorld>`
  

Class Methods
=============

.. class:: World

	.. function:: World *GetActiveWorld() const

		Returns the currently active world, or nullptr if there is no active world.

Instance Methods
================

.. class:: World

	.. function:: World(SceneManager *sceneManager)

		Creates a new world using the given scene manager.

		.. note:: The scene manager must not be nullptr!

	.. function:: World(const std::string& sceneManager)

		Creates a new world using the given scene manager name. The name must be the class name of a class subclassing :cpp:class`SceneManager` that is registered with the runtime class catalogue.

	.. function:: void Update(float delta)

		Called when the world is asked to do a step. This method is called each frame and can be used to do additional update steps before any of the scene nodes within the world are updated.

		:param delta: The time since the last frame. Can be used for frame rate independent movement

	.. function:: void UpdateEditMode(float delta)

		Called when the world is asked to do a step while in edit mode

	.. function:: void DidUpdateToFrame(FrameID frame)

		Called at the end of each frame, after all scene nodes have been updated but before they are rendered.

	.. function:: void AddSceneNode(SceneNode *node)

		Adds the given scene node to the world. This call will fail if the scene node is already tracked by the world, or if it's already tracked by another world.

	.. function:: void RemoveSceneNode(SceneNode *node)

		Removes the given scene node from the world. This call will fail if the scene node isn't tracked by the world.

	.. function:: void DropSceneNodes()

		Removes all scene nodes currently tracked by the world.

	.. function:: void ApplyNodes()

		Worlds are lazy updating, adding a new node is processed only as much as necessary and the bulk of propagation work is deferred until the end of the frame when all new nodes are processed at once. This can have the side effect of for example adding a new node that should be processed by a physics attachment, which is then immediately used, but which hasn't made it to the physics attachment yet. This can be avoided by calling this method, which forces all new nodes to be applied immediately.

	.. function:: void AddAttachment(WorldAttachment *attachment)

		Adds the given world attachment to the world

	.. function:: void RemoveAttachment(WorldAttachment *attachment)

		Removes the given world attachment from the world

	.. function:: void LoadOnThread(Thread *thread, Deserializer *deserializer)

		Called when the world should either load from a serialized state, or recreate/load by other means. The default implementation must be invoked in order to provide correct deserialization of the world. When this method is called, the world just became the active world and all newly created scene nodes will be added to it.

		:param thread: The thread the method is invoked on.
		:param deserializer: The deserializer from which to load. Can be `nullptr`

		.. seealso:: :cpp:func:`World::SupportsBackgroundLoading`
		.. note:: This method should be overriden by subclasses

	.. function:: void FinishLoading(Deserializer *deserializer)

		Called on the main thread after the :cpp:func:`World::LoadOnThread` completed and can be used to finalize the loading.

	.. function:: bool SupportsBackgroundLoading() const

		If this method returns false (default true), the :cpp:func:`World::LoadOnThread` method will be called on the main thread, otherwise it will be called on a background thread. You are strongly encouraged to support background loading as to not block the main thread and have it still handle events and additionally display a loading screen to the user, or similar.

	.. function:: void SaveOnThread(Thread *thread, Serializer *serializer)

		Called when the world should serialize its current state into the serializer.

	.. function:: FinishSaving(Serializer *serializer)

		Called on the main thread to give the world a chance to finalize the saving process.

	.. function:: bool SupportsBackgroundSaving() const

		If this method returns false (default is false), the :cpp:func:`World::SaveOnThread` method will be called on the main thread. Note that saving doesn't stop the world from updating, which is why the default is to block the main thread and stop updating the world. Special consideration have to be made to support background saving!

	.. function:: SceneManager *GetSceneManager() const

		Returns the scene manager of the world

	.. function:: Array *GetSceneNodes()

		Returns all scene nodes that are in the world.

	.. function:: T *GetSceneNodeWithTag(Tag tag)

		Returns the first scene node with a given tag, which also inherits from the provided class. For example, calling `GetSceneNodeWithTag<Decal>(2)` will return the first Decal with a tag of 2.


		The full signature for the method is:

		.. code:: cpp

			template<class T>
			T *GetSceneNodeWithTag(Tag tag)

	.. function:: Array *GetSceneNodesWithTag(Tag tag)

		Returns all scene nodes with the given tag and which inherit from the given class.


		The full signature for the method is:

		.. code:: cpp

			template<class T>
			Array *GetSceneNodesWithTag(Tag tag)

	.. function:: void SetMode(Mode mode)

		Sets the mode of the world

	.. function:: Mode GetMode() const

		Returns the current mode of the world

					
Constants
=========

.. class:: World 

	.. type:: Mode
		
		* :code:`Play` Default mode describing a normal game world
		* :code:`Edit` Edit mode, used for worlds which are being edited
