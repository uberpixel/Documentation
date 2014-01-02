.. _rnscenenode.rst:

*************************
SceneNode class reference
*************************

.. namespace:: RN
.. class:: SceneNode 

+---------------------+--------------------------------------+
|  **Inherits from**  | :cpp:class:`Object`                  |
+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNSceneNode.h                        |
+---------------------+--------------------------------------+

Overview
========

The SceneNode class implements the root class for objects that can be placed into a scene. Scene nodes have a position, rotation and scale that defines their spatial orientation within the scene. They also implement the core concepts of interacting with objects within your scene, and provide a common interface that simplifies tasks like manipulating a scene, creating dependency chains and synchronizing with other nodes across thread boundaries.

Scene nodes also build the base for all objects that want to implement any kind of logic and/or interaction with the scene itself. For this purpose, the scene node provides a method called :cpp:func:`Update <SceneNode::Update>` which will be invoked every frame and that subclasses can override to implement their own logic.

Scene nodes implement just a basic set of functionality that is common to all objects within a scene, their functionality is extended by concrete subclasses, see also :cpp:class:`Entity`, :cpp:class:`Light` and :cpp:class:`Camera`.

Dependency chains and update fine tuning
----------------------------------------

Scene nodes allow you to create explicit and implicit dependency chains that alter the order in which they get updated. This is useful in cases where you want to tightly define the order in which scene nodes get updated, for example, let's say you have a third person camera class that follows another scene node. You want the camera to update after the other scene node does to avoid having the camera randomly lag a frame behind. You can do so by calling :cpp:func:`AddDependency(otherNode) <SceneNode::AddDependency>` on the camera. As long as the dependency exists, the camera will not be updated until the other node has finished updating. This is synchronized across threads and done automatically, so simply declaring a dependency on another scene node is everything you need to do. There are also implicit dependencies; Child scene nodes will not update until their parents have updated.

If you don't require this kind of specialized update fine tuning, you can also set the priority of the scene node by calling :cpp:func:`SetPriority`. This allows you to set the update priority in terms of three well defined and fenced categories, that is, if you declare your scene node as `Priority::UpdateEarly`, it will be guaranteed to have updated before any other update category.

If you require super fine granularity, you can also override the :cpp:func:`CanUpdate <SceneNode::CanUpdate>` method and implement your own logic in there. Note though that you should call the super classes `CanUpdate` method in any case, and if you need to wait for another scene node, you should strongly consider using dependencies instead, since they trigger scene graph optimizations that are not possible otherwise.

Children
--------

Scene nodes can have any number of other scene nodes attached to them, although a scene node can only have one parent at a time. Child scene nodes will move relative to their parents, that is, when you rotate a scene node, all children will be rotated relative to it by the same amount as well. As already mentioned, children have an implicit dependency on their parent.

Attachments
-----------

Scene nodes can also have any number of attachments. Attachments are observer/manipulators of their housing scene node; They will receive callbacks when their parent moves around or is updated in another way, and they can also alter their parents orientation within the scene. Additionally, attachments also receive an Update message every frame. Attachments are used for example for physics engines, where the physics engine provides eg. a rigid body implementation as attachment, which will then move the scene node around with it.

Tasks
=====

Construction
------------

* :cpp:func:`SceneNode() <SceneNode::SceneNode>`
* :cpp:func:`SceneNode(const Vector3& position) <SceneNode::SceneNode>`
* :cpp:func:`SceneNode(const Vector3& position, const Quaternion& rotation) <SceneNode::SceneNode>`
  
Spatial Modification
--------------------

* :cpp:func:`Translate(const Vector3& trans) <SceneNode::Translate>`
* :cpp:func:`Scale(const Vector3& scal) <SceneNode::Scale>`
* :cpp:func:`Rotate(const Vector3& rot) <SceneNode::Rotate>`
* :cpp:func:`TranslateLocal(const Vector3& trans) <SceneNode::TranslateLocal>`
* :cpp:func:`ScaleLocal(const Vector3& scal) <SceneNode::ScaleLocal>`
* :cpp:func:`virtual SetPosition(const Vector3& pos) <SceneNode::SetPosition>`
* :cpp:func:`virtual SetScale(const Vector3& scal) <SceneNode::SetScale>`
* :cpp:func:`virtual SetRotation(const Quaternion& rot) <SceneNode::SetRotation>`
* :cpp:func:`virtual SetWorldPosition(const Vector3& pos) <SceneNode::SetWorldPosition>`
* :cpp:func:`virtual SetWorldScale(const Vector3& scal) <SceneNode::SetWorldScale>`
* :cpp:func:`virtual SetWorldRotation(const Quaternion& rot) <SceneNode::SetWorldRotation>`
* :cpp:func:`LookAt(SceneNode *other) <SceneNode::LookAt>`
* :cpp:func:`GetPosition() const <SceneNode::GetPosition>`
* :cpp:func:`GetScale() const <SceneNode::GetScale>`
* :cpp:func:`GetEulerAngle() const <SceneNode::GetEulerAngle>`
* :cpp:func:`GetRotation() const <SceneNode::GetRotation>`
* :cpp:func:`Forward() const <SceneNode::Forward>`
* :cpp:func:`Up() const <SceneNode::Up>`
* :cpp:func:`Right() const <SceneNode::Right>`
* :cpp:func:`GetWorldPosition() const <SceneNode::GetWorldPosition>`
* :cpp:func:`GetWorldScale() const <SceneNode::GetWorldScale>`
* :cpp:func:`GetWorldEulerAngle() const <SceneNode::GetWorldEulerAngle>`
* :cpp:func:`GetWorldRotation() const <SceneNode::GetWorldRotation>`
* :cpp:func:`GetWorldTransform() const <SceneNode::GetWorldTransform>`
* :cpp:func:`GetLocalTransform() const <SceneNode::GetLocalTransform>`

Modification
------------

* :cpp:func:`SetFlags(Flags flags) <SceneNode::SetFlags>`
* :cpp:func:`SetBoundingBox(const AABB& boundingBox, bool calculateBoundingSphere) <SceneNode::SetBoundingBox>`
* :cpp:func:`SetBoundingSphere(const Sphere& boundingSphere) <SceneNode::SetBoundingSphere>`
* :cpp:func:`SetPriority(Priority priority) <SceneNode::SetPriority>`
* :cpp:func:`SetAction(const std::function& action) <SceneNode::SetAction>`
* :cpp:func:`virtual Update(float delta) <SceneNode::Update>`
* :cpp:func:`GetFlags() const <SceneNode::GetFlags>`
* :cpp:func:`GetLastFrame() const <SceneNode::GetLastFrame>`
* :cpp:func:`GetWorld() const <SceneNode::GetWorld>`
* :cpp:func:`GetPriority() const <SceneNode::GetPriority>`

Working with children
---------------------

* :cpp:func:`AttachChild(SceneNode *child) <SceneNode::AttachChild>`
* :cpp:func:`DetachChild(SceneNode *child) <SceneNode::DetachChild>`
* :cpp:func:`DetachFromParent() <SceneNode::DetachFromParent>`
* :cpp:func:`GetChildren() const <SceneNode::GetChildren>`
* :cpp:func:`GetParent() const <SceneNode::GetParent>`

Working with attachments
------------------------

* :cpp:func:`AddAttachment(SceneNodeAttachment *attachment) <SceneNode::AddAttachment>`
* :cpp:func:`RemoveAttachment(SceneNodeAttachment *attachment) <SceneNode::RemoveAttachment>`
* :cpp:func:`GetAttachment(MetaClassBase *metaClass) const <SceneNode::GetAttachment>`
* :cpp:func:`GetAttachment() const <SceneNode::GetAttachment>`
* :cpp:func:`GetAttachments() const <SceneNode::GetAttachments>`

Synchronization
---------------

* :cpp:func:`AddDependency(SceneNode *dependency) <SceneNode::AddDependency>`
* :cpp:func:`RemoveDependency(SceneNode *dependency) <SceneNode::RemoveDependency>`
* :cpp:func:`virtual CanUpdate(FrameID frame) <SceneNode::CanUpdate>`
* :cpp:func:`LockChildren() const <SceneNode::LockChildren>`
* :cpp:func:`UnlockChildren() const <SceneNode::UnlockChildren>`

Callbacks
---------

* :cpp:func:`virtual ChildDidUpdate(SceneNode *child, uint32 changes) <SceneNode::ChildDidUpdate>`
* :cpp:func:`virtual ChildWillUpdate(SceneNode *child, uint32 changes) <SceneNode::ChildWillUpdate>`
* :cpp:func:`virtual WillAddChild(SceneNode *child) <SceneNode::WillAddChild>`
* :cpp:func:`virtual DidAddChild(SceneNode *child) <SceneNode::DidAddChild>`
* :cpp:func:`virtual WillRemoveChild(SceneNode *child) <SceneNode::WillRemoveChild>`
* :cpp:func:`virtual DidRemoveChild(SceneNode *child) <SceneNode::DidRemoveChild>`


Instance Methods
================

.. class:: SceneNode

	.. function:: SceneNode()

		The designated constructor. Initializes the position to `0|0|0` and scale to `1|1|1`.

	.. function:: SceneNode(const Vector3& position)

		The designated constructor. Initializes the position to `position` and scale to `1|1|1`.

	.. function:: SceneNode(const Vector3& position, const Quaternion& rotation)

		The designated constructor. Initializes the position to `position`, scale to `1|1|1` and rotation to `rotation`.


	.. function:: void SetAction(const std::function<>& action)

		Sets the internal action to the given function. This allows creating actions for scene nodes without the need to subclass them (note though that you are strongly encouraged to create a proper subclass for performance reasons).

		.. note::

			The action must have the following signature: `void (SceneNode *node, float delta)`

	.. function:: void Update(float delta)

		This method is automatically called every frame and gives the scene node the chance to update itself. The default implementation simply invokes the scene nodes action (if set).

		After the update method ran, the scene nodes internal frame counter will be updated to the current frame.

		.. note::

			Subclasses are strongly encouraged to call their superclasses Update method!

		.. note::

			This method may be called on ANY thread.

	.. function:: void AddAttachment(SceneNodeAttachment *attachment)

		Adds the given attachment to the receiver. The attachment must not be attached to another scene node.

	.. function:: void RemoveAttachment(SceneNodeAttachment *attachment)

		Removes the given attachment from the receiver

	.. function:: SceneNodeAttachment *GetAttachment(MetaClassBase *metaClass) const

		Returns the first attachment that inherits from the given class, or nullptr if there is no attachment that matches the given class. Note, if there are multiple attachments that inherit from the given class, the returned attachment is undefined.

	.. function:: T *GetAttachment() const

		Returns the first attachment that inherits from the given class. This is a convenience template function.

		.. admonition:: Example

			.. code:: cpp

				SceneNode *foo = ..;
				MyAttachment *attachment = foo->GetAttachment<MyAttachment>();

	.. function:: Array *GetAttachments() const

		Returns all attachments that of the receiver.

	.. function:: bool CanUpdate(FrameID frame)

		This method allows subclasses to defer their update until a later point in time. The World will repeatedly ask the scene node if it can update to the given frame, and only if it returns `true` will the :cpp:func:`Update <SceneNode::Update>` be invoked. For performance reasons, you are strongly encouraged to not override this method and instead use dependencies and/or priorities to alter the update time.

		However, if you do override this method, call the superclasses implementation first and check its value before performing your own logic. Also make sure to not perform heavy tasks in this method since it may be called many times per frame.
		
Constants
=========

.. class:: SceneNode 

	.. type:: Priority
		
		* :code:`UpdateEarly` The scene node is updated at the beginning of the frame
		* :code:`UpdateDontCare` The scene node is updated sometimes between early and late
		* :code:`UpdateLate` The scene node is updated at the end of the frame

	.. type:: Flags

		Flags can be ORed together

		* :code:`FlagDrawLate` The scene node will be rendered after all other scene nodes
		* :code:`FlagStatic` The scene node won't receive update methods. This allows for potential fast paths of static objects and should be set for all that don't require their Update method to be invoked (they can still be moved around freely, the only limitation are updates)
		* :code:`FlagHidden` The scene node and all its children will be culled away and not rendered
		* :code:`FlagHideChildren` The scene nodes children will be culled
		 
		.. seealso:: :cpp:func:`SetFlags`

	.. type:: ChangeSet

		A change set describes a set of one or more changes that were or will be applied to a scene node. Multiple changes might be ORed together

		* :code:`ChangedGeneric` A generic change (can be anything BUT a change that has an explicit constant)
		* :code:`ChangedFlags`  A change to the scene nodes flags
		* :code:`ChangedPosition` A change to the scene nodes position, rotation or scale
		* :code:`ChangedDependencies` A change to the scene nodes dependencies
		* :code:`ChangedPriority` A change to the scene nodes priority
		* :code:`ChangedParent` A change to the scene nodes parent
		* :code:`ChangedAttachments` A change to the scene nodes attachments
		* :code:`ChangedWorld` A change to the scene nodes world
