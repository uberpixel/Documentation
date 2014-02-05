.. _rnmaterial.rst:

************************
Material class reference
************************

.. namespace:: RN
.. class:: Material 

+---------------------+--------------------------------------+
|  **Inherits from**  | :cpp:class:`Object`                  |
+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNMaterial.h                         |
+---------------------+--------------------------------------+

Overview
========

The Material class encapsulates the properties for rendering. A material holds references to the texture(s), the shader, colours and various other properties such as the blending, cull mode etc.

Materials and post processing
-----------------------------

Cameras have the ability to use their own material to render a scene. This material, will disable any custom material that would otherwise be used for rendering and instead the camera will always pick the surface material for rendering. However, often times it's more desirable to have a "combined" material, for instance, while the surface material can provide the shader and ambient colour, the material that would be used normally should provide the discard and culling mode. For these cases, materials have an override property which they can use to selectively override properties of a surface material, and a surface material too can use the override property to selectively pick which properties should be used.

Tasks
=====

Construction
------------

* :cpp:func:`Material() <Material::Material>`
* :cpp:func:`Material(Shader *shader) <Material::Material>`
* :cpp:func:`Material(const Material *other) <Material::Material>`
  
Rendering properties
--------------------

* :cpp:func:`AddTexture(Texture *texture) <Material::AddTexture>`
* :cpp:func:`InsertTexture(Texture *texture, size_t index) <Material::InsertTexture>`
* :cpp:func:`ReplaceTexture(Texture *Texture, size_t index) <Material::ReplaceTexture>`
* :cpp:func:`RemoveTexture(Texture *texture) <Material::RemoveTexture>`
* :cpp:func:`RemoveTextures() <Material::RemoveTextures>`
* :cpp:func:`SetLighting(bool enabled) <Material::SetLighting>`
* :cpp:func:`SetCullMode(CullMode mode) <Material::SetCullMode>`
* :cpp:func:`SetPolygonMode(PolygonMode mode) <Material::SetPolygonMode>`
* :cpp:func:`SetBlending(bool enabled) <Material::SetBlending>`
* :cpp:func:`SetBlendEquation(BlendEquation equation) <Material::SetBlendEquation>`
* :cpp:func:`SetBlendMode(BlendMode source, BlendMode destination) <Material::SetBlendMode>`
* :cpp:func:`SetPolygonOffset(bool enabled) <Material::SetPolygonOffset>`
* :cpp:func:`SetPolygonOffsetFactor(float factor) <Material::SetPolygonOffsetFactor>`
* :cpp:func:`SetPolygonOffsetUnits(float units) <Material::SetSetPolygonOffsetUnits>`
* :cpp:func:`SetAmbientColor(const Color &color) <Material::SetAmbientColor>`
* :cpp:func:`SetDiffuseColor(const Color &color) <Material::SetDiffuseColor>`
* :cpp:func:`SetSpecularColor(const Color &color) <Material::SetSpecularColor>`
* :cpp:func:`SetEmissiveColor(const Color &color) <Material::SetEmissiveColor>`
* :cpp:func:`SetDepthTest(bool enabled) <Material::SetDepthTest>`
* :cpp:func:`SetDepthWrite(bool enabled) <Material::SetDepthWrite>`
* :cpp:func:`SetDepthTestMode(DepthMode mode) <Material::SetDepthTestMode>`
* :cpp:func:`SetDiscard(bool enabled) <Material::SetDiscard>`
* :cpp:func:`SetDiscardThreshold(float threshold) <Material::SetDiscardThreshold>`
* :cpp:func:`SetOverride(Override override) <Material::SetOverride>`
* :cpp:func:`GetTextures() const <Material::GetTextures>`
* :cpp:func:`GetLighting() const <Material::GetLighting>`
* :cpp:func:`GetCullMode() const <Material::GetCullMode>`
* :cpp:func:`GetPolygonMode() const <Material::GetPolygonMode>`
* :cpp:func:`GetBlending() const <Material::GetBlending>`
* :cpp:func:`GetBlendEquation() const <Material::GetBlendEquation>`
* :cpp:func:`GetBlendSource() const <Material::GetBlendSource>`
* :cpp:func:`GetBlendDestination() const <Material::GetBlendDestination>`
* :cpp:func:`GetPolygonOffset() const <Material::GetPolygonOffset>`
* :cpp:func:`GetPolygonOffsetFactor() const <Material::GetPolygonOffsetFactor>`
* :cpp:func:`GetPolygonOffsetUnits() const <Material::GetPolygonOffsetUnits>`
* :cpp:func:`GetAmbientColor() const <Material::GetAmbientColor>`
* :cpp:func:`GetDiffuseColor() const <Material::GetDiffuseColor>`
* :cpp:func:`GetSpecularColor() const <Material::GetSpecularColor>`
* :cpp:func:`GetEmissiveColor() const <Material::GetEmissiveColor>`
* :cpp:func:`GetDepthTest() const <Material::GetDepthTest>`
* :cpp:func:`GetDepthWrite() const <Material::GetDepthWrite>`
* :cpp:func:`GetDepthTestMode() const <Material::GetDepthTestMode>`
* :cpp:func:`GetDiscard() const <Material::GetDiscard>`
* :cpp:func:`GetDiscardThreshold() const <Material::GetDiscardThreshold>`
* :cpp:func:`GetOverride() const <Material::GetOverride>`

Shader modifications
--------------------

* :cpp:func:`SetShader(Shader *shader) <Material::SetShader>`
* :cpp:func:`GetShader() const <Material::GetShader>`
* :cpp:func:`Define(const std::string &define) <Material::Define>`
* :cpp:func:`Define(const std::string &define, const std::string &value) <Material::Define>`
* :cpp:func:`Define(const std::string &define, int32 value) <Material::Define>`
* :cpp:func:`Define(const std::string &define, float value) <Material::Define>`
* :cpp:func:`Undefine(const std::string &define) <Material::Undefine>`
* :cpp:func:`AddShaderUniform(Args &&... args) <Material::AddShaderUniform>`
* :cpp:func:`ApplyUniforms(ShaderProgram *program) <Material::ApplyUniforms>`
* :cpp:func:`GetLookup() const <Material::GetLookup>`

Instance Methods
================

.. class:: Material

	.. function:: Material()

		Creates a material without any textures or shader. The resulting material is unfit for rendering since rendering requires at least a shader to be set.

	.. function:: Material(Shader *shader)

		Creates a material with the given shader.

	.. function:: Material(const Material *material)

		Creates a copy of the material. Note that this results in a shallow copy, ie, both materials will reference the same textures instead of having separate copies of them.

	.. function:: void AddTexture(Texture *texture)

		Adds the texture to the end of the texture array of the receiver

	.. function:: void InsertTexture(Texture *texture, size_t index)

		Inserts the texture at the given index of the texture array of the receiver

	.. function:: void ReplaceTexture(Texture *texture, size_t index)

		Replaces the texture at the given index of the texture array of the receiver

	.. function:: void RemoveTexture(Texture *texture)

		Removes the texture from the texture array. This method is a no-op if the texture isn't present

	.. function:: void RemoveTextures()

		Removes all textures from the receiver

	.. function:: void SetLighting(bool enabled)

		Enables or disables the lighting property of the receiver. If this is set to true, lighting is enabled and when rendering, the material will be considered by the light manager of the rendering camera (if available).

		The lighting property itself doesn't explicitly affect rendering but only requests that rendering with this material uses lighting through the light manager. Light rendering also requires that the material uses a shader that supports lighting and that the rendering camera has a light manager.

		Default is `true`.

	.. function:: void SetCullMode(CullMode cullMode)

		Sets the cull mode of the receiver. Default is back face culling.

	.. function:: void SetPolygonMode(PolygonMode mode)

		Sets the polygon fill mode of the receiver. This value affects how polygons rendered using the material will be filled, default are filled polygons.

		.. Note:: Setting this to line or point mode will severely affect performance

	.. function:: void SetBlending(bool enabled)

		Enables or disables blending of the material. Blending is disabled by default, and is further affected by the blend mode that.

	.. function:: void SetBlendEquation(BlendEquation equation)

		Sets the blend equation of the receiver. Default is additive.

	.. function:: void SetBlendMode(BlendMode source, BlendMode destination)

		Sets the blend mode of the receiver. This value affects how the source pixels are blended with the destination pixels, ie the ones already present in the frame buffer.

	.. function:: void SetAmbientColor(const Color &ambient)

		Sets the ambient color of the receiver

	.. function:: void SetDiffuseColor(const Color &diffuse)

		Sets the diffuse color of the receiver

	.. function:: void SetSpecularColor(const Color &specular)

		Sets the specular color of the receiver 

	.. function:: void SetEmissiveColor(const Color &emissive)

		Sets the emissive color of the receiver

	.. function:: void SetDepthTest(bool enabled)

		Sets wether the material should render with depth testing enabled or not.

	.. function:: void SetDepthWrite(bool enabled)

		Sets wether the material writes into the depth buffer when rendering

	.. function:: void SetDepthTestMode(DepthMode mode)

		Sets the depth testing mode of the receiver

	.. function:: void SetDiscard(bool enabled)

		Sets wether the material should render using discard. If this is enabled and the alpha value of a rendered pixel is smaller than the discard threshold of the material, the pixel will be discarded.

		.. note:: This isn't an actual OpenGL property but needs to be supported by the shader. This property, as well as the discard threshold are only used as a hint for the renderer what shader program to use when rendering.

	.. function:: void SetDiscardThreshold(float threshold)

		Sets the discard threshold of the material.

	.. function:: void SetOverride(Override override)

		Sets the material override of the receiver. When the material is used as camera material, this property tells the renderer which properties it should use from the normal material. When the material is used as a normal material, this property is used to tell the renderer which properties to use from it instead of the camera material.

	.. function:: const Array *GetTextures() const

		Returns the textures of the material

	.. function:: bool GetLighting() const

		Returns if the material wants to be rendered with lighting.

	.. function:: CullMode GetCullMode() const

		Returns the cull mode of the material

	.. function:: PolygonMode GetPolygonMode() const

		Returns the polygon mode of the receiver

	.. function:: bool GetBlending() const

		Returns true if the material uses blending, otherwise false

	.. function:: BlendEquation GetBlendEquation() const

		Returns the blend equation of the receiver

	.. function:: BlendMode GetBlendSource() const

		Returns the blend mode for the source fragment

	.. function:: BlendMode GetBlendDestination() const

		Returns the blend mode for the destination fragment, ie, the one already in the framebuffer

	.. function:: const Color &GetAmbientColor() const

		Returns the ambient colour

	.. function:: const Color &GetDiffuseColor() const

		Returns the diffuse colour

	.. function:: const Color &GetSpecularColor() const

		Returns the specular colour

	.. function:: const Color &GetEmissiveColor() const

		Return the emissive colour

	.. function:: bool GetDepthTest() const

		Returns true if the material renders with depth test, otherwise false

	.. function:: bool GetDepthWrite() const

		Returns true if the material renders with depth writing enabled, otherwise false

	.. function:: DepthMode GetDepthTestMode() const

		Returns the depth test mode of the material

	.. function:: bool GetDiscard() const

		Returns true if the material renders with discard enabled or not

	.. function:: float GetDiscardThreshold() const

		Returns the discard threshold used when rendering with discard enabled

	.. function:: Override GetOverride() const

		Returns the override mask of the material

	.. function:: void SetShader(Shader *shader)

		Sets the shader of the material. A material requires a shader in order to be rendered.

	.. function:: Shader *GetShader() const

		Returns the shader of the receiver

	.. function:: void Define(const std::string &define)

		Adds the given define to the shader defines of the receiver. Unlike defines set directly on the shader, these defines are only used when rendering with the material.

	.. function:: void Define(const std::string &define, const std::string &value)

		Adds the given define as the given string value

	.. function:: void Define(const std::string &define, int32 value)

		Adds the given define as the given integer value

	.. function:: void Define(const std::string &define, float value)

		Adds the given define as the given float value

	.. function:: void Undefine(const std::string &define)

		Removes the given define from the receiver.

	.. function:: ShaderUniform *AddShaderUniform(Args && args, ...)

		Adds a new shader uniform in place forwarding the given arguments. The arguments must be a valid constructor signature of the ShaderUniform class.

	.. function:: void ApplyUniforms(ShaderProgram *program)

		Applies the uniforms of the material to the shader program. Calling this should rarely be needed unless when writing a custom renderer. The shader program must be bound already and the call must happen on the OpenGL queue.

	.. function:: const ShaderLookup &GetLookup() const

		Returns the shader program lookup for the receiver. This method is only useful in the context of custom rendering or pre-fetching certain shader programs.

Constants
=========

.. class:: Material 

	.. type:: Override

		* :code:`Culling` Overrides the cull mode property
		* :code:`Blending` Overrides the blending property
		* :code:`Blendequation` Overrides the blend equation proeprty
		* :code:`Blendmode` Overrides the source and destination blend mode properties
		* :code:`Ambient` Overrides the ambient color
		* :code:`Diffuse` Overrides the diffuse color
		* :code:`Specular` Overrides the specular color
		* :code:`Emissive` Overrides the emissive color
		* :code:`Depthtest` Overrides the depth test property
		* :code:`DepthtestMode` Overrides the depth test mode property
		* :code:`DepthWrite` Overrides the depth write property
		* :code:`Discard` Overrides the discard property
		* :code:`DiscardThreshold` Overrides the discard threshold property
		* :code:`Textures` Overrides the textures
		* :code:`PolygonOffset` Overrides the polygon offset, polygon offset factor and polygon offset unit properties
		* :code:`PolygonMode` Overrides the polygon mode
		* :code:`GroupBlending` Overrides the blending, blend equation and blend mode
		* :code:`GroupDiscard` Overrides the discard, discard threshold and textures
	
	.. type:: CullMode

		* :code:`None` No culling
		* :code:`BackFace` Back face culling
		* :code:`FrontFace` Front face culling

	.. type:: DepthMode

		* :code:`Never` Never passes the depth test
		* :code:`Always` Always passes the depth test
		* :code:`Less` Passes the depth test if the depth value is less than the one in the depth buffer
		* :code:`LessOrEqual` Passes the depth test if the depth value is less than or equal to the one in the depth buffer
		* :code:`Equal` Passes the depth test if the depth value is equal to the one in the depth buffer
		* :code:`NotEqual` Passes the depth test if the depth value is unequal to the one in the depth buffer
		* :code:`Greater` Passes the depth test if the depth value is greater than the one in the depth buffer
		* :code:`GreatorOrEqual` Passes the depth test if the depth value is greater than or equal to the one in the depth buffer
	
	.. type:: PolygonMode

		* :code:`Points` Draw points where the vertices are
		* :code:`Lines` Draw lines along the edges of polygons
		* :code:`Fill` Fill polygons
	
	.. type:: BlendMode

		The blend mode is used to blend the rendered pixel together with the pixel already present in the frame buffer. The equation consists out of three parts; The source blend mode, the destination blend mode and the blend equation. In the following table it is assumed that the blend equation is set to additive. `X` is used for every color channel, except of explicitly mentioned ones. Ie X = 0; A = 1 means that the red, green and blue channels are 0  while the alpha channel is 1. A `s` prefix means that the source pixel is used, a `d` prefix means the destination pixel.

		* :code:`Zero` X * 0
		* :code:`One`  X * 0
		* :code:`SourceColor` X * sX
		* :code:`OneMinusSourceColor` X * (1 - sX)
		* :code:`SourceAlpha` X * sA
		* :code:`OneMinusSourceAlpha` X * (1 - sA)
		* :code:`DestinationColor` X * dX
		* :code:`OneMinusDestinationColor` X * (1 - dX)
		* :code:`DestinationAlpha` X * dA
		* :code:`OneMinusDestinationAlpha` X * (1 - dA)
	
	.. type:: BlendEquation

		The blend equation is used to determine how to combine the source and destination pixels calculated using the blend mode to form the final pixel that is written in the frame buffer.

		* :code:`Add` sX + dX
		* :code:`Subtract` sX - dX
		* :code:`ReverseSubtract` dX - sX
		* :code:`Min` min(sX, dX)
		* :code:`Max` max(sX, dX)
