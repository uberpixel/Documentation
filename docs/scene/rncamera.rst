.. _rncamera.rst:

**********************
Camera class reference
**********************

.. namespace:: RN
.. class:: Camera 

+---------------------+--------------------------------------+
|  **Inherits from**  | :cpp:class:`SceneNode`               |
+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNCamera.h                           |
+---------------------+--------------------------------------+

Overview
========

The Camera class is a special kind of SceneNode that renders the scene into a render storage. Optionally, the rendered result can be flushed onto the screen and/or be re-used in a post processing pipeline. Additionally, it also allows a high degree of customization for the composition of the final rendering result of a frame.

Post processing pipelines
-------------------------

By default, cameras just draw the scene from their current position and orientation, however, they can also be chained together into so called post processing pipelines. A post processing pipeline is attached to a root camera which is responsible for rendering the scene initially, though the root camera is not limited to having only one post processing pipeline attached to it. You can then add additional cameras to a post processing pipeline as a so called stage, where each stage either re-renders the scene or takes the result of a previous stage or camera to further process it. This way you can easily build post processing effects like bloom, SSAO and FXAA.

Frame composition
-----------------

Rayne doesn't directly render cameras onto the screen, but instead renders them into their backing storage, which contains a combination of zero or more color buffers, zero or one depth buffer and zero or one stencil buffer. After rendering every camera and evaluating their post processing pipelines, all cameras marked as flushable cameras will be blitted onto the screen using their blit shader and blit mode.

When creating a new camera, it is automatically added to the scene as rendering camera and thus becomes a camera that will be flushed. The order in which cameras render, and later flush the scene depends on their priority; Cameras with a higher priority will be rendered before cameras with lower priority. A camera ceases being flushed when it becomes either the parent of a post processing pipeline, or it is added as a stage to a post processing pipeline. You can enforce cameras being flushed by setting their `ForceFlush` flag, likewise, you can disable flushing of any camera by setting their `NoFlush` flag. By default, only the last stage within a complete post processing pipeline is flushed to the screen.

Tasks
=====

Construction
------------

* :cpp:func:`Camera() <Camera::Camera>`
* :cpp:func:`Camera(const Vector2 &size) <Camera::Camera>`
* :cpp:func:`Camera(const Vector2 &size, Texture *target) <Camera::Camera>`
* :cpp:func:`Camera(const Vector2 &size, Texture *target, Flags flags) <Camera::Camera>`
* :cpp:func:`Camera(const Vector2 &size, Texture *target, Flags flags, RenderStorage::BuferFormat fomrat) <Camera::Camera>`
* :cpp:func:`Camera(const Vector2 &size, Texture::Format targetFormat) <Camera::Camera>`
* :cpp:func:`Camera(const Vector2 &size, Texture::Format targetFormat, Flags flags) <Camera::Camera>`
* :cpp:func:`Camera(const Vector2 &size, Texture::Format targetFormat, Flags flags, RenderStorage::BufferFormat format, float scaleFactor = 0.0f) <Camera::Camera>`
* :cpp:func:`Camera(const Vector2 &size, RenderStorage *storage, Flags flags, float scaleFactor = 0.0f) <Camera::Camera>`

Rendering
---------

* :cpp:func:`SetFrame(const Rect& frame) <Camera::SetFrame>`
* :cpp:func:`SetRenderingFrame(const Rect& frame) <Camera::SetRenderingFrame>`
* :cpp:func:`SetFlags(Flags flags) <Camera::SetFlags>`
* :cpp:func:`SetClearColor(const Color& color) <Camera::SetClearColor>`
* :cpp:func:`SetClearMask(ClearMask mask) <Camera::SetClearMask>`
* :cpp:func:`SetColorMask(ColorMask mask) <Camera::SetColorMask>`
* :cpp:func:`SetMaterial(Material *material) <Camera::SetMaterial>`
* :cpp:func:`SetRenderStorage(RenderStorage *storage) <Camera::SetRenderStorage>`
* :cpp:func:`SetLightManager(LightManager *lightManager) <Camera::SetLightManager>`
* :cpp:func:`SetSky(Model *sky) <Camera::SetSky>`
* :cpp:func:`SetLODCamera(Camera *camera) <Camera::SetLODCamera>`
* :cpp:func:`SetFOV(float fov) <Camera::SetFOV>`
* :cpp:func:`SetAspectRatio(float ratio) <Camera::SetAspectRatio>`
* :cpp:func:`SetClipNear(float near) <Camera::SetClipNear>`
* :cpp:func:`SetClipFar(float far) <Camera::SetClipFar>`
* :cpp:func:`SetFogColor(Color color) <Camera::SetFogColor>`
* :cpp:func:`SetFogNear(float near) <Camera::SetFogNear>`
* :cpp:func:`SetFogFar(float far) <Camera::SetFogFar>`
* :cpp:func:`SetAmbientColor(Color color) <Camera::SetAmbientColor>`
* :cpp:func:`SetClipPlane(Vector4 clipPlane) <Camera::SetClipPlane>`
* :cpp:func:`SetRenderGroups(RenderGroups groups) <Camera::SetRenderGroups>`
* :cpp:func:`SetOrthogonalFrustum(float top, float bottom, float left, float right) <Camera::SetOrthogonalFrustum>`
* :cpp:func:`PrepareForRendering(Renderer *renderer) <Camera::PrepareForRendering>`
* :cpp:func:`GetStorage() const <Camera::GetStorage>`
* :cpp:func:`GetClearColor() const <Camera::GetClearColor>`
* :cpp:func:`GetFrame() <Camera::GetFrame>`
* :cpp:func:`GetRenderingFrame() <Camera::GetRenderingFrame>`
* :cpp:func:`GetMaterial() const <Camera::GetMaterial>`
* :cpp:func:`GetFlags() const <Camera::GetFlags>`
* :cpp:func:`GetLODCamera() const <Camera::GetLODCamera>`
* :cpp:func:`GetSky() const <Camera::GetSky>`
* :cpp:func:`GetLightManager() const <Camera::GetLightManager>`
* :cpp:func:`GetPriority() const <Camera::GetPriority>`
* :cpp:func:`GetBlitShader() const <Camera::GetBlitShader>`
* :cpp:func:`GetBlitMode() const <Camera::GetBlitMode>`
* :cpp:func:`GetRenderGroups() const <Camera::GetRenderGroups>`
* :cpp:func:`GetFOV() const <Camera::GetFOV>`
* :cpp:func:`GetAspectRatio() const <Camera::GetAspectRatio>`
* :cpp:func:`GetClipNear() const <Camera::GetClipNear>`
* :cpp:func:`GetClipFar() const <Camera::GetClipFar>`
* :cpp:func:`GetFogNear() const <Camera::GetFogNear>`
* :cpp:func:`GetFogFar() const <Camera::GetFogFar>`
* :cpp:func:`GetFogColor() const <Camera::GetFogColor>`
* :cpp:func:`GetAmbientColor() const <Camera::GetAmbientColor>`
* :cpp:func:`GetClipPlane() const <Camera::GetClipPlane>`

Projection & Frustum
--------------------

* :cpp:func:`ToWorld(const Vector3& dir) <Camera::ToWorld>`
* :cpp:func:`InFrustum(const Vector3& position, float radius) <Camera::InFrustum>`
* :cpp:func:`InFrustum(const Sphere& sphere) <Camera::InFrustum>`
* :cpp:func:`InFrustum(const AABB& aabb) <Camera::InFrustum>`
* :cpp:func:`GetFrustumCenter() <Camera::GetFrustumCenter>`
* :cpp:func:`GetFrustumRadius() <Camera::GetFrustumRadius>`
* :cpp:func:`GetProjectionMatrix() <Camera::GetProjectionMatrix>`
* :cpp:func:`GetInverseProjectionMatrix() <Camera::GetInverseProjectionMatrix>`
* :cpp:func:`GetViewMatrix() <Camera::GetViewMatrix>`
* :cpp:func:`GetInverseViewMatrix() <Camera::GetInverseViewMatrix>`

Post Processing
---------------

* :cpp:func:`AddPostProcessingPipeline(const std::string& name) <Camera::AddPostProcessingPipeline>`
* :cpp:func:`AddPostProcessingPipeline(PostProcessingPipeline *pipeline) <Camera::AddPostProcessingPipeline>`
* :cpp:func:`RemovePostProcessingPipeline(PostProcessingPipeline *pipeline) <Camera::RemovePostProcessingPipeline>`
* :cpp:func:`GetPostProcessingPipeline(const std::string& name) const <Camera::GetPostProcessingPipeline>`
* :cpp:func:`GetPostProcessingPipelines() const <Camera::GetPostProcessingPipelines>`


Instance Methods
================

.. class:: Camera

	.. function:: void SetFrame(const Rect& frame)

		Sets the frame of the receiver. A cameras frame is the portion of its storage it will render into, allowing multiple cameras to render into different parts of a shared render storage.

		If the `UpdateStorageFrame` flag is set, the camera will update its underlying storage frame to fit its own frame.

	.. function:: void SetRenderingFrame(const Rect& frame)

		Sets the rendering frame of the receiver. The rendering frame determines where the camera is flushed into, either on the screen or into a post processing pipeline. By default this is equal to the cameras frame, and it can be forced back to the default by setting an empty rect.

		.. seealso:: :cpp:func:`SetBlitMode() <Camera::SetBlitMode>`

	.. function:: void SetFlags(Flags flags)

		Sets the flags of the receiver.

	.. function:: void SetClearColor(const Color& color)

		Sets the clear color of the receiver.

		.. seealso:: :cpp:func:`SetClearMask() <Camera::SetClearMask>`

	.. function:: void SetClearMask(ClearMask mask)

		Sets the clear mask of the receiver, which determines which parts of the underlying storage the camera should clear before it renders into it. Setting this to 0 will stop the camera from clearing its storage, which can be useful when the camera shares its storage with another camera and renders into it after the other camera.

		By default the clear mask is enabled for all buffers; Color, depth and stencil.

		.. note:: Disabling clearing may be associated with a small performance overhead. This penalty only occurs if the underlying storage is never cleared before it's getting rendered into for the first time of a frame.

	.. function:: void SetColorMask(ColorMask mask)

		Sets the color mask of the receiver, which allows selectively enabling and disabling of color channels when rendering. By default, all color channels are enabled.

	.. function:: void SetMaterial(Material *material)

		Sets the material of the camera to the given material. Cameras with a set material will render the using the given material instead of the individual materials set per scene node. Scene node materials can selectively override some properties of the post processing material via their :cpp:member:`override <Material::override>` property, for example to force discard rendering or similar.

	.. function:: void SetRenderStorage(RenderStorage *storage)

		Sets a new render storage for the receiver. The new render storage mustn't be NULL.

	.. function:: void SetLightManager(LightManager *lightmanager)

		Sets a new light manager for the receiver. This can be set to nullptr to disable light rendering for the camera, otherwise the camera will render lights using its light manager.

	.. function:: void SetSky(Model *sky)

		Sets a new sky model for the receiver. This can be nullptr to disable sky rendering. The sky will always be rendered using its first LOD stage, and is always drawn before anything.

	.. function:: void SetLODCamera(Camera *lodCamera)

		Sets the LOD camera of the receiver. By default, this is set to NULL which forces the LOD system to use the camera itself for LOD stage selection. If a LOD camera is set, the LOD camera will be used instead to select the LOD stage.

	.. function:: void SetFOV(float fov)

		Sets the field of view in degrees of the virtual eye of the camera. Defaults to 70°

	.. function:: void SetAspectRatio(float aspect)

		Sets the aspect ration of the receiver. This method becomes a no-op if `Flags::UpdateAspect` is set.

	.. function:: void SetClipNear(float near)

		Sets the near clip plane. This parameter should be as high as possible, defaults to 0.1f

	.. function:: void SetClipFar(float far)

		Sets the far clip plane. This parameter should be as low as possible, defaults to 500.0f

	.. function:: void SetFogColor(const Color& color)

		Sets the fog color of the receiver. To enable fog rendering, you also need to set the `Flags::UseFog` flag.

		.. seealso:: 
					| :cpp:func:`SetFogFar` 
					| :cpp:func:`SetFogNear` 

	.. function:: void SetFogFar(float far)

		Sets the far point of the fog, ie where the fog becomes completely opaque

	.. function:: void SetFogNear(float near)

		Sets the near point of the fog, ie the distance where fog starts to become visible

	.. function:: void SetAmbientColor(const Color& ambient)

		Sets the ambient color of the receiver

	.. function:: void SetClipPlane(const Vector4& planes)

		Sets the clip planes of the receiver. The clip planes are enabled only when the `Flags::UseClipPlanes` flag is set.

	.. function:: void SetRenderGroups(RenderGroups groups)

		Sets the mask of render groups of the receiver. Ie, a camera with `RenderGroups::Group0` and `RenderGroups::Group2` set will only render scene nodes that have either 0 or 2 as their render group.

		.. seealso:: :cpp:func:`SceneNode::SetRenderGroup <SceneNode::SetRenderGroup>`

	.. function:: void SetOrthogonalFrustum(float top, float bottom, float left, float right)

		Sets the orthogonal frustum of the receiver. This method has only an effect when the cameras `Flag::Orthogonal` is set, ie the camera is an orthogonal camera.

	.. function:: void PrepareForRendering(Renderer *renderer)

		Prepares the camera for rendering. This updates the underlying storage, clears the buffers and binds the framebuffer for rendering. Calling this function isn't normally needed unless when writing a custom renderer, where it's needed to call this function before trying to render into the camera.

	.. function:: RenderStorage *GetStorage() const

		Returns the underlying render storage of the camera

	.. function:: const Color &GetClearColor() const

		Return the clear color of the camera

	.. function:: const Rect &GetFrame()

		Returns the frame of the camera

		.. seealso:: :cpp:func:`SetFrame <Camera::SetFrame>`

	.. function:: Rect GetRenderingFrame()

		Returns the rendering frame of the camera, by default this is the same as the cameras frame

		.. seealso:: :cpp:func:`SetRenderingFrame <Camera::SetRenderingFrame>`

	.. function:: Material *GetMaterial() const

		Returns the material of the camera or nullptr

	.. function:: Flags GetFlags() const

		Returns the receivers flags

	.. function:: Camera *GetLODCamera() const

		Returns the LOD camera, if set, or otherwise the `this` pointer.

		.. note:: This method always returns a valid camera that you should use when calculating LOD stages

	.. function:: Model *GetSky() const

		Returns the Sky model of the receiver or nullptr

	.. function:: LightManager *GetLightManager()

		Returns the light manager of the receiver or nullptr if non is set. By default, a camera has a :cpp:class:`ClusteredLightManager`.

	.. function:: int32 GetPriority() const

		Returns the rendering priority of the receiver. Defaults to 0.

	.. function:: Shader *GetBlitShader() const

		Returns the blit shader of the camera, the returned shader is always non null.

	.. function:: BlitMode GetBlitMode() const

		Returns the blit mode of the receiver

	.. function:: RenderGroups GetRenderGroups() const

		Returns the render groups of the receiver

	.. function:: float GetFOV() const

		Returns the field of view of the virtual eye in degrees

	.. function:: float GetAspectRatio() const

		Returns the aspect ratio of the receiver

	.. function:: float GetClipNear() const

		Returns the near clip plane of the receiver

	.. function:: float GetClipFar() const

		Return the far clip plane of the receiver

	.. function:: float GetFogFar() const

		Returns the currently set far point of the fog, ie where the fog becomes completely opaque

	.. function:: float GetFogNear() const

		Returns the currently set near point of the fog, ie the distance where fog starts to become visible

	.. function:: const Color &GetFogColor() const

		Returns the fog color of the receiver. To enable fog rendering, you also need to set the `Flags::UseFog` flag.

	.. function:: const Color &GetAmbientColor() const

		Returns the ambient color of the receiver

	.. function:: const Vector4 &GetClipPlane() const

		Returns the clip plane of the receiver

	.. function:: Vector3 ToWorld(const Vector3 &dir)

		Converts the given vector from view space of the receiver into world space. The `x` and `y` axis of the direction are in view space, while the `z` axis is in world space.

	.. function:: bool InFrustum(const Vector3 &position, float radius)

		Returns true if the sphere at `position` with `radius` is within the view frustum of the receiver.

	.. function:: bool InFrustum(const Sphere &sphere)

		Returns true if the given sphere is within the view frustum of the receiver

	.. function:: bool InFrustum(const AABB &aabb)

		Returns true if the given axis aligned bounding box is within the view frustum of the receiver

		.. note:: This function is slower than a sphere based check, which should be preferred in almost all cases

	.. function:: const Vector3 &GetFrustumCenter()

		Returns the center of the view frustum of the receiver

	.. function:: float GetFrustumRadius()

		Returns the radius of the view frustum of the receiver

	.. function:: const Matrix &GetProjectionMatrix()

		Returns the projection matrix of the receiver.

	.. function:: const Matrix &GetInverseProjectionMatrix()

		Returns the inverse projection matrix of the receiver

	.. function:: const Matrix &GetViewMatrix()

		Returns the view matrix of the receiver

	.. function:: const Matrix &GetInverseViewMatrix()

		Returns the inverse view matrix of the receiver

	.. function:: PostProcessingPipeline *AddPostProcessingPipeline(const std::string& name)

		Attempts to add a new post processing pipeline to the receiver. If the names is already taken, it will throw an `InvalidArgumentException` exception, otherwise it will return a pointer to the newly added pipeline.

	.. function:: void AddPostProcessingPipeline(PostProcessingPipeline *pipeline)

		Attempts to add the given post processing pipeline to the receiver. If a pipeline with the name already exists, or if the pipeline is already attached to a camera, this method will throw an `InvalidArgumentException`.

	.. function:: void RemovePostProcessingPipeline(PostProcessingPipeline *pipeline)

		Removes the given post processing pipeline from the receiver. The post processing pipeline is implicitly deleted when the function succeeds, if it fails because the pipeline wasn't added to the receiver, the call become a no-op.

	.. function:: PostProcessingPipeline *GetPostProcessingPipeline(const std::string& name)

		Returns the post processing pipeline with the given name, or nullptr if no pipeline with such a name exists.

		.. note::

			Though this method is atomic, the returned pipeline can be deleted when another thread calls :cpp:func:`RemovePostProcessingPipeline() <Camera::RemovePostProcessingPipeline>` after the method returns and before you are done using the pipeline. If you need a guarantee that the pipeline is not implicitly deleted on another thread, you must call :cpp:func:`Lock() <Object::Lock>` on the receiver and :cpp:func:`Unlock() <Object::Unlock>` when you are done using it.

	.. function:: const std::vector<PostProcessingPipeline *>& GetPostProcessingPipelines()

		Returns the post processing pipelines currently added to the receiver.

		.. note::

			This method is not thread safe, if you need a guarantee that the returned vector isn't altered on another thread while you are using it, you must call :cpp:func:`Lock() <Object::Lock>` on the receiver and :cpp:func:`Unlock() <Object::Unlock>` when you are done using it.
  
Constants
=========

.. class:: Camera 

	.. type:: Flags

		Flags can be ORed together

		* :code:`UpdateAspect` When the camera frame changes, it will automatically update its aspect ratio
		* :code:`UpdateStorageFrame` When the camera frame changes, it will automatically update its backing storages frame as well
		* :code:`NoSky` The camera won't render any sky, not even when inherited through a post processing stage
		* :code:`NoSorting` The camera won't sort scene nodes prior to rendering, meaning that everything is rendered in the order it was send to the renderer
		* :code:`NoRender` The camera won't render the scene
		* :code:`NoFlush` The camera will not be flushed into the final frame buffer.
		* :code:`NoDepthWrite` Disables writing into the depth buffer when the camera renders. Can be used to re-use the depthbuffer of a previous depth pre-pass.
		* :code:`ForceFlush` The camera will be flushed into the final frame buffer, no matter where it is in the post processing pipeline. This flag takes precedence over the `NoFlush` flag.
		* :code:`InheritPosition` The camera will inherit its position from the parent camera in the post processing pipeline its attached to (only used when the camera is a post processing stage)
		* :code:`InheritFrame` The camera will inherit its frame from the parent camera in the post processing pipeline its attached to (only used when the camera is a post processing stage)
		* :code:`InheritFrame` The camera will inherit its projection matrix from the parent camera in the post processing pipeline its attached to (only used when the camera is a post processing stage)
		* :code:`Fullscreen` The camera will automatically update its frame to fit onto the whole rendering surface
		* :code:`Orthogonal` If set, the camera will use an orthogonal projection for rendering
		* :code:`UseFog` If set, the camera will render fog
		* :code:`UseClipPlanes` If set, the camera will use its clip plane
		* :code:`Defaults` A default set of flags, includes `Fullscreen`, `UpdateAspect`, `UpdateStorageFrame`, `UseFog`
		* :code:`Inherit` A default set of flags for post processing stages, includes `InheritFrame`, `InheritPosition`, `InheritProjection`
		 
		.. seealso:: :cpp:func:`SetFlags`

	.. type:: ClearMask

		A clear mask describes which parts of its storage a camera should clear to default values before rendering. Masks can be ORed together.

		* :code:`Color` The camera will clear the color buffer to its clear color
		* :code:`Depth` The camera will clear the depth buffer
		* :code:`Stencil` The camera will clear the stencil buffer
		
		.. seealso:: :cpp:func:`SetClearMask`
		
	.. type: ColorMask

		A color mask describes which color channels should be enabled when rendering a camera. Masks can be ORed together.

		* :code:`Red` Red channel
		* :code:`Green` Green channel
		* :code:`Blue` Blue channel
		* :code:`Alpha` Alpha channel

		.. seealso:: :cpp:func:`SetColorMask`
