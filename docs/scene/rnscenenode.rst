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
* :cpp:func:`TranslateLocal(const Vector3& trans) <SceneNode::TranslateLocal>`
* :cpp:func:`Scale(const Vector3& scal) <SceneNode::Scale>`
* :cpp:func:`Rotate(const Vector3& rot) <SceneNode::Rotate>`
* :cpp:func:`LookAt(const RN::Vector3 &target, bool keepUpAxis=false) <SceneNode::LookAt>`
* :cpp:func:`virtual SetPosition(const Vector3& pos) <SceneNode::SetPosition>`
* :cpp:func:`virtual SetScale(const Vector3& scal) <SceneNode::SetScale>`
* :cpp:func:`virtual SetRotation(const Quaternion& rot) <SceneNode::SetRotation>`
* :cpp:func:`virtual SetWorldPosition(const Vector3& pos) <SceneNode::SetWorldPosition>`
* :cpp:func:`virtual SetWorldScale(const Vector3& scal) <SceneNode::SetWorldScale>`
* :cpp:func:`virtual SetWorldRotation(const Quaternion& rot) <SceneNode::SetWorldRotation>`
* :cpp:func:`GetPosition() const <SceneNode::GetPosition>`
* :cpp:func:`GetScale() const <SceneNode::GetScale>`
* :cpp:func:`GetEulerAngle() const <SceneNode::GetEulerAngle>`
* :cpp:func:`GetRotation() const <SceneNode::GetRotation>`
* :cpp:func:`GetTransform() const <SceneNode::GetTransform>`
* :cpp:func:`GetForward() const <SceneNode::GetForward>`
* :cpp:func:`GetUp() const <SceneNode::GetUp>`
* :cpp:func:`GetRight() const <SceneNode::GetRight>`
* :cpp:func:`GetWorldPosition() const <SceneNode::GetWorldPosition>`
* :cpp:func:`GetWorldScale() const <SceneNode::GetWorldScale>`
* :cpp:func:`GetWorldEulerAngle() const <SceneNode::GetWorldEulerAngle>`
* :cpp:func:`GetWorldRotation() const <SceneNode::GetWorldRotation>`
* :cpp:func:`GetWorldTransform() const <SceneNode::GetWorldTransform>`

Modification
------------

* :cpp:func:`SetFlags(Flags flags) <SceneNode::SetFlags>`
* :cpp:func:`SetBoundingBox(const AABB& boundingBox, bool calculateBoundingSphere=true) <SceneNode::SetBoundingBox>`
* :cpp:func:`SetBoundingSphere(const Sphere& boundingSphere) <SceneNode::SetBoundingSphere>`
* :cpp:func:`SetRenderGroup(uint8 group) <SceneNode::SetRenderGroup>`
* :cpp:func:`SetCollisionGroup(uint8 group) <SceneNode::SetCollisionGroup>`
* :cpp:func:`SetPriority(Priority priority) <SceneNode::SetPriority>`
* :cpp:func:`SetAction(const std::function& action) <SceneNode::SetAction>`
* :cpp:func:`virtual Update(float delta) <SceneNode::Update>`
* :cpp:func:`GetFlags() const <SceneNode::GetFlags>`
* :cpp:func:`GetBoundingBox() const <SceneNode::GetBoundingBox>`
* :cpp:func:`GetBoundingSphere() const <SceneNode::GetBoundingSphere>`
* :cpp:func:`GetRenderGroup() const <SceneNode::GetRenderGroup>`
* :cpp:func:`GetCollisionGroup() const <SceneNode::GetCollisionGroup>`
* :cpp:func:`GetPriority() const <SceneNode::GetPriority>`
* :cpp:func:`GetLastFrame() const <SceneNode::GetLastFrame>`
* :cpp:func:`GetWorld() const <SceneNode::GetWorld>`

Working with children
---------------------

* :cpp:func:`AddChild(SceneNode *child) <SceneNode::AddChild>`
* :cpp:func:`RemoveChild(SceneNode *child) <SceneNode::RemoveChild>`
* :cpp:func:`RemoveFromParent() <SceneNode::RemoveFromParent>`
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

Callbacks
---------

* :cpp:func:`virtual ChildWillUpdate(SceneNode *child, ChangeSet changes) <SceneNode::ChildWillUpdate>`
* :cpp:func:`virtual ChildDidUpdate(SceneNode *child, ChangeSet changes) <SceneNode::ChildDidUpdate>`
* :cpp:func:`virtual WillAttachChild(SceneNode *child) <SceneNode::WillAddChild>`
* :cpp:func:`virtual DidAttachChild(SceneNode *child) <SceneNode::DidAddChild>`
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

	.. function:: void Translate(const Vector3& trans)

		Move the scene node with the given translation vector in world coordinates or if it has a parent within the parents coordinate system.

	.. function:: void TranslateLocal(const Vector3& trans)

		Move the scene node with the given translation vector along the scene nodes own coordinate System.

		.. admonition:: Example

			.. code:: cpp

				// Move along the scene nodes forward direction
				TranslateLocal(RN::Vector3(0.0f, 0.0f, -1.0f));

				// Move along the scene nodes right direction
				TranslateLocal(RN::Vector3(1.0f, 0.0f, 0.0f));

				// Move along the scene nodes up direction
				TranslateLocal(RN::Vector3(0.0f, 1.0f, 0.0f));

	.. function:: void Scale(const Vector3& scal)

		Change the scene nodes scale along the different axes within its own coordinate system.

	.. function:: void Rotate(const Vector3& rot)

		Rotate the scene node within its own coordinate system with the given yaw, pitch and roll angle.

		.. admonition:: Example

			.. code:: cpp

				void RotatingCoin::Update(float delta)
				{
					// Rotate around its y-axis with 16 degrees per second
					Rotate(RN::Vector3(16.0f*delta, 0.0f, 0.0f));
				}

	.. function:: void LookAt(const RN::Vector3 &target, bool keepUpAxis=false)

		Rotate the scene node to look at the target position.
		If keepUpAxis is set to true, it will only rotate around its up vector.

	.. function:: void SetPosition(const Vector3& pos)

		Set the scene node to the position given in pos. This will be within the parents coordinate system or the world if there is none.

	.. function:: void SetScale(const Vector3& scal)

		Set the scene nodes scale to the given scale. This will be effected by the parents scale if there is one.

	.. function:: void SetRotation(const Quaternion& rot)

		Set the scene nodes rotation to the given rotation. This will be effected by the parents rotation if there is one.

	.. function:: void SetWorldPosition(const Vector3& pos)

		Set the scene nodes position to the given position. This will compensate the parents transformations if there is one.

	.. function:: void SetWorldScale(const Vector3& scal)

		Set the scene nodes scale to the given scale. This will compensate the parents transformations if there is one.

	.. function:: void SetWorldRotation(const Quaternion& rot)

		Set the scene nodes rotation to the given rotation. This will compensate the parents transformations if there is one.

	.. function:: Vector3 GetPosition() const

		Returns the scene nodes position within its parents coordinate system or the worlds coordinate system if there is no parent.

	.. function:: Vector3 GetScale() const

		Returns the scene nodes scale within its parents coordinate system or the worlds coordinate system if there is no parent.

	.. function:: Vector3 GetEulerAngle() const

		Returns the scene nodes rotation in yaw-pitch-roll euler angles within its parents coordinate system or the worlds coordinate system if there is no parent.

	.. function:: Quaternion GetRotation() const

		Returns the scene nodes rotation within its parents coordinate system or the worlds coordinate system if there is no parent.

	.. function:: Matrix GetTransform() const

		Returns the scene nodes transformation matrix in its parents space if there is one, in world space otherwise.

	.. function:: Vector3 GetForward() const

		Returns a vector pointing into the scene nodes coordinate systems forward (0, 0, -1) direction within world coordinates.

	.. function:: Vector3 GetUp() const

		Returns a vector pointing into the scene nodes coordinate systems up (0, 1, 0) direction within world coordinates.

	.. function:: Vector3 GetRight() const

		Returns a vector pointing into the scene nodes coordinate systems right (1, 0, 0) direction within world coordinates.

	.. function:: Vector3 GetWorldPosition() const

		Returns the position of the scene node within the world.

	.. function:: Vector3 GetWorldScale() const

		Returns the scale of the scene node within the world.

	.. function:: Vector3 GetWorldEulerAngle() const

		Returns the rotation as yaw, pitch and roll angle of the scene node within the world.

	.. function:: Quaternion GetWorldRotation() const

		Returns the rotation of the scene node within the world.

	.. function:: Matrix GetWorldTransform() const

		Returns the scene nodes transformation matrix in world space.

	.. function:: void SetFlags(Flags flags)

		Allows to set one or more flags for the scene node.

		.. seealso:: :cpp:type:`Flags`

		.. admonition:: Example

			.. code:: cpp

				// Render the scene node after everything else and don´t call its update method
				SetFlags(Flags::FlagDrawLate | Flags::FlagStatic);

	.. function:: void SetBoundingBox(const AABB& boundingBox, bool calculateBoundingSphere=true)

		Allows to set a custom bounding box and if calculateBoundingSphere is set, a bounding sphere covering the box will automatically be set.

	.. function:: void SetBoundingSphere(const Sphere& boundingSphere)

		Allows to set a custom bounding sphere which will be used for culling.

	.. function:: void SetRenderGroup(uint8 group)

		Cameras can specify which render groups they render. So this feature can be used to hide a scene node in some cameras while rendering it in others.

		.. admonition:: Example

			.. code:: cpp

				// Create a camera and set its render groups
				RN::Camera *reflectionCamera = new RN::Camera();
				reflectionCamera->SetRenderGroups(RN::Camera::RenderGroups::Group0);

				// Have only node1 rendered by reflectionCamera
				node1->SetRenderGroup(0);
				node2->SetRenderGroup(1);

	.. function:: void SetCollisionGroup(uint8 group)

		This is currently only used to specify what scene nodes a ray cast can hit.

	.. function:: void SetPriority(Priority priority)

		This can be used to set an update priority for the scene node.
		The default value is UpdateDontCare, but can be changed to schedule the scene nodes update earlier or later.

		.. seealso:: :cpp:type:`Priority`

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

	.. function:: Flags GetFlags() const

		Returns the currently set flags of the scene node.

	.. function:: AABB GetBoundingBox() const

		Returns the scene nodes bounding box.

	.. function:: Sphere GetBoundingSphere() const

		Returns the scene nodes bounding sphere.

	.. function:: uint8 GetRenderGroup() const

		Returns the scene nodes render group.

	.. function:: uint8 GetCollisionGroup() const

		Returns the scene nodes collision group.

	.. function:: Priority GetPriority() const

		Returns the scene nodes priority.

	.. function:: FrameID GetLastFrame() const

		Returns the ID of the last frame for which the update function definitely finished.

	.. function:: World *GetWorld() const

		Returns the pointer to the world, but only after it is fully loaded and attached, which might take several frames. It will return nullptr otherwise.

	.. function:: void AddChild(SceneNode *child)

		The given child will be attached to this scene node. This means that this scene nodes transformations will also effect the childs transformations. Both scene nodes will keep their current transformation within the world.

		.. admonition:: Example

			.. code:: cpp

				// Create the games first person camera
				RN::Camera *camera = new RN::Camera();

				// Create a spot light
				RN::Light *spotLight = new RN::Light(RN::Light::Type::SpotLight);

				// Attach the spot light to the camera
				camera->AddChild(spotLight);

				// Move the light a bit to the bottom right
				spotLight->SetPosition(RN::Vector3(1.0f, -0.5f, 0.0f));

				// Now move the camera and the light will just move with it
				camera->TranslateLocal(RN::Vector3(0.0f, 0.0f, -2.0f));

	.. function:: void RemoveChild(SceneNode *child)

		If the given child is currently attached to the scene node, it will be detached. Both scene nodes will keep their transformation within the world.

	.. function:: void RemoveFromParent()

		Detaches the scene node from its parent if it has one. Both, this scene node and its parent will keep their transformation within the world.

	.. function:: const Array *GetChildren() const

		Returns the array of currently attached children. This might be empty if there is no child attached.

	.. function:: SceneNode *GetParent() const

		Returns the parent if the scene node has one, nullptr otherwise.

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

		Returns all attachments of the receiver.

	.. function:: void AddDependency(SceneNode *dependency)

		Adds the given scene node as dependency. This will make sure that the dependency will be updated before this scene node.

	.. function:: void RemoveDependency(SceneNode *dependency)

		Removes the given dependency from the this scene nodes dependencies.

	.. function:: bool CanUpdate(FrameID frame)

		This method allows subclasses to defer their update until a later point in time. The World will repeatedly ask the scene node if it can update to the given frame, and only if it returns `true` will the :cpp:func:`Update <SceneNode::Update>` be invoked. For performance reasons, you are strongly encouraged to not override this method and instead use dependencies and/or priorities to alter the update time.

		However, if you do override this method, call the superclasses implementation first and check its value before performing your own logic. Also make sure to not perform heavy tasks in this method since it may be called many times per frame.

	.. function:: void ChildWillUpdate(SceneNode *child, ChangeSet changes)

		This callback will be called before the given child is going to have the changes applied.

	.. function:: void ChildDidUpdate(SceneNode *child, ChangeSet changes)

		This callback will be called after the given child had the changes applied.
		
	.. function:: void WillAddChild(SceneNode *child)

		This callback will be called before the given child is added to this scene node.

	.. function:: void DidAddChild(SceneNode *child)

		This callback will be called after the given child was added to this scene node.

	.. function:: void WillRemoveChild(SceneNode *child)

		This callback will be called before the given child is removed from this scene node.

	.. function:: void DidRemoveChild(SceneNode *child)

		This callback will be called after the given child was removed from this scene node.
		
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
