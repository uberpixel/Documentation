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

The World class encapsulates a complete scene, and means to load and save it. It also provides mechanism to listen for changes within a scene, for example added or removed scene nodes, via the :cpp:class:`WorldAttachment` class. Lastly, together with a scene manager, it provides the means required to render a scene, by tracking all :cpp:class`Camera`s within it and rendering them via the scene manager.

Subclassing
-----------

While a World by itself already provides a number of useful implementations, it's usually a good idea to create one or more subclasses that take care of loading and/or saving of the world, or creating the world entirely through code. Even though these operations are common to all worlds, it's impossible to provide a common implementation for them. The World class allows you to define your own, custom and specialized level format that can then be loaded by a custom subclass, allowing a great deal of flexibility.

Most likely you'll want to subclass the :cpp:func:`LoadOnThread() <World::LoadOnThread>` and :cpp:func:`SupportsBackgroundLoading() <World::SupportsBackgroundLoading>` methods to define your loading and/or scene creation mechanism.

Scene nodes and the active world
--------------------------------

Newly created scene nodes are automatically added to the currently active world, so there is no need to do this manually. They can, however, be removed from their world and inserted into another, non-active one. Simply creating a World doesn't automatically make it the active one, it first has to be made active via the :cpp:class`WorldCoordinator` singleton, which is also the reason it's not encouraged to start creating or loading the World within its constructor. Instead, the :cpp:func:`LoadOnThread() <World::LoadOnThread>` method should be used for that.

Tasks
=====

Construction
------------

* :cpp:func:`World(SceneManager *sceneManager) <World::World>`
* :cpp:func:`World(const std::string &sceneManager) <World::World>`

Driving the world
-----------------

* :cpp:func:`virtual Update(float delta) <World::Update>`
* :cpp:func:`virtual DidUpdateToFrame(FrameID frame) <World::DidUpdateToFrame>`

Handling scene nodes
--------------------

* :cpp:func:`SetReleaseSceneNodesOnDestruction(bool releaseSceneNodes) <World::SetReleaseSceneNodesOnDestruction>`
* :cpp:func:`AddSceneNode(SceneNode *node) <World::AddSceneNode>`
* :cpp:func:`RemoveSceneNode(SceneNode *node) <World::RemoveSceneNode>`
* :cpp:func:`DropSceneNodes() <World::DropSceneNodes>`

Attachments
-----------

* :cpp:func:`AddAttachment(WorldAttachment *attachment) <World::AddAttachment>`
* :cpp:func:`RemoveAttachment(WorldAttachment *attachment) <World::RemoveAttachment>`

Loading and Saving
------------------

* :cpp:func:`virtual LoadOnThread(Thread *thread) <World::LoadOnThread>`
* :cpp:func:`virtual FinishLoading() <World::FinishLoading>`
* :cpp:func:`virtual SupportsBackgroundLoading() const <World::SupportsBackgroundLoading>`

Misc
----

* :cpp:func:`GetSceneManager() const <World::GetSceneManager>`
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

	.. function:: void DidUpdateToFrame(FrameID frame)

		Called at the end of each frame, after all scene nodes have been updated but before they are rendered.

	.. function:: void SetReleaseSceneNodesOnDestruction(bool releaseSceneNodes)

		If set to true (default), the World will take ownership of all created scene nodes that it tracks. When it's deleted, it will automatically invoke :cpp:func`Release() <Object::Release>` on each scene node.

	.. function:: void AddSceneNode(SceneNode *node)

		Adds the given scene node to the world. This call will fail if the scene node is already tracked by the world, or if it's already tracked by another world.

	.. function:: void RemoveSceneNode(SceneNode *node)

		Removes the given scene node from the world. This call will fail if the scene node isn't tracked by the world.

	.. function:: void DropSceneNodes()

		Removes all scene nodes currently tracked by the world.

		.. seealso:: :cpp:func:`World::SetReleaseSceneNodesOnDestruction`

	.. function:: void AddAttachment(WorldAttachment *attachment)

		Adds the given world attachment to the world

	.. function:: void RemoveAttachment(WorldAttachment *attachment)

		Removes the given world attachment from the world

	.. function:: void LoadOnThread(Thread *thread)

		Called when the world should either load from a serialized state, or recreate/load by other means. The default implementation does nothing and doesn't need to be invoked. When this method is called, the world just became the active world and all newly created scene nodes will be added to it.

		:param thread: The thread the method is invoked on.
		
		.. seealso:: :cpp:func:`World::SupportsBackgroundLoading`
		.. note:: This method should be overriden by subclasses

	.. function:: void FinishLoading()

		Called on the main thread after the :cpp:func:`World::LoadOnThread` completed and can be used to finalize the loading.

	.. function:: bool SupportsBackgroundLoading() const

		If this method returns false (default true), the :cpp:func:`World::LoadOnThread` method will be called on the main thread, otherwise it will be called on a background thread. You are strongly encouraged to support background loading as to not block the main thread and have it still handle events and additionally display a loading screen to the user, or similar.

	.. function:: SceneManager *GetSceneManager() const

		Returns the scene manager of the world
		