.. _rnshaderprogram.rst:

*****************************
ShaderProgram class reference
*****************************

.. namespace:: RN
.. class:: ShaderProgram

+-------------------+------------+
| **Inherits from** |    None    |
+-------------------+------------+
| **Availability**  | Rayne 1.0  |
+-------------------+------------+
| **Declared in**   | RNShader.h |
+-------------------+------------+

Overview
========

A ShaderProgream encapsulates a completely compiled and linked shader program that can be used for rendering. It's immutable and created through the :cpp:class:`Shader` class. A ShaderProgram shouldn't be cached since the source shader object may invalidate it later on, instead, it should be requested again from the source shader object which will maintain a cache to it.

The default uniform locations described in the `Properties`_ section are automatically resolved using their name, eg, `matProj` will contain the uniform location of the uniform named `matProj` in the shader, if it exists. Additionally, these default built in uniforms are automatically bound to the right data by the renderer.

Tasks
=====

Requesting information
----------------------

* :cpp:func:`HasGeometryShader() const <ShaderProgram::HasGeometryShader>`
* :cpp:func:`HasTessellationShader() const <ShaderProgram::HasTessellationShader>`
* :cpp:func:`GetLocation(const std::string &name) <ShaderProgram::GetLocation>`


Instance Methods
================

.. class:: ShaderProgram
	
	.. function:: bool HasGeometryShader() const

		Returns true if the shader program has a linked geometry shader

	.. function:: bool HasTessellationShader() const

		Returns true if the shader program has linked tessellation shaders

	.. function:: GLuint GetLocation(const std::string &name)

		Returns the location of the uniform with the given name, or -1 if the uniform doesn't exist. This method should be favoured over calling `glGetUniformLocation()` as it maintains a cache of already resolved uniform locations.

Properties
==========

.. class:: ShaderProgram

	.. member:: GLuint program

		The handle to the OpenGL program

	.. member:: GLuint matProj

		The uniform location where the projection matrix is bound to.

	.. member:: GLuint matProjInverse

		The uniform location where the inverse projection matrix is bound to.

	.. member:: GLuint matView

		The uniform location where the view matrix is bound to

	.. member:: GLuint matViewInverse

		The uniform location where the inverse view matrix is bound to

	.. member:: GLuint matModel

		The uniform location where the model matrix is bound to

	.. member:: GLuint matModelInverse

		The uniform location where the inverse model matrix is bound to

	.. member:: GLuint matNormal

		The uniform location where the rotation matrix is bound to

	.. member:: GLuint matNormalInverse

		The uniform location where the inverse rotation matrix is bound to

	.. member:: GLuint matViewModel

		The uniform location where the view model matrix is bound to

	.. member:: GLuint matViewModelInverse

		The uniform location where the inverse view model matrix is bound to

	.. member:: GLuint matProjView

		The uniform location where the projection view matrix is bound to

	.. member:: GLuint matProjViewInverse

		The uniform location where the inverse projection view matrix is bound to

	.. member:: GLuint matProjViewModel

		The uniform location where the projection view model matrix is bound to

	.. member:: GLuint matProjViewModelInverse

		The uniform location where the inverse projection view model matrix is bound to

	.. member:: GLuint matBones

		The uniform location where the animation bone matrices are bound to

	.. member:: GLuint instancingData

		The uniform location where the instancing transform data is bound to

	.. member:: GLuint instancingIndices

		The uniform location where the instancing indices lookup table is bound to

	.. member:: GLuint attPosition

		The position vertex attribute location

	.. member:: GLuint attNormal

		The normal vertex attribute location

	.. member:: GLuint attTangent

		The tangent vertex attribute location

	.. member:: GLuint attTexcoord0

		The first UV set vertex attribute location

	.. member:: GLuint attTexcoord1

		The second UV set vertex attribute location

	.. member:: GLuint attColor0

		The first color set vertex attribute location

	.. member:: GLuint attColor1

		The second color set vertex attribute location

	.. member:: GLuint attBoneWeights

		The bone weight vertex attribute location

	.. member:: GLuint attBoneIndices

		The bone indices vertex attribute location

	.. member:: GLuint time

		Uniform location where the time since the application start is bound to (float)

	.. member:: GLuint frameSize

		Uniform location where the dimension of the rendering frame is bound to (vec4)

	.. member:: GLuint clipPlanes

		Uniform location where the clip plane is bound to (vec4)

	.. member:: GLuint discardThreshold

		Uniform location where the discard threshold is bound to (float)

	.. member:: GLuint fogPlanes

		Uniform location where the fog planes are bound to (vec4)

	.. member:: GLuint fogColor

		Uniform location where the fog color is bound to (vec4)

	.. member:: GLuint cameraAmbient

		Uniform location where the camera ambient is bound to (vec4)

	.. member:: GLuint ambient

		Uniform location where the ambient color of the material is bound to (vec4)

	.. member:: GLuint diffuse

		Uniform location where the diffuse color of the material is bound to (vec4)

	.. member:: GLuint specular

		Uniform location where the specular color of the material is bound to (vec4)

	.. member:: GLuint emissive

		Uniform location where the emissive color of the material is bound to (vec4)

	.. member:: GLuint viewPosition

		Uniform location where the camera position is bound to (vec3)

	.. member:: GLuint viewNormal

		Uniform location where the camera normal is bound to (vec3)

	.. member:: std::vector<GLuint> texlocations

		Vector with the texture uniform locations. Textures are automatically bound to the shader uniforms with names `mTexture0` to `mTexture31`, though names can be skipped (ie `mTexture0`, `mTexture2` to only have the first and third texture of the material bound).

	.. member:: std::vector<GLuint> texinfolocations

		Vector with the texture info locations. Similar naming as the texture location vector, but with `Info` appended. Eg `mTexture0Info`. The uniforms are a vec4  with the dimension of the texture bound to it.
