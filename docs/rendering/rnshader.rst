.. _rnshader.rst:

**********************
Shader class reference
**********************

.. namespace:: RN
.. class:: Shader

+---------------------+----------------------------+
|  **Inherits from**  |    :cpp:class:`Object`     |
+---------------------+----------------------------+
| **Availability**    | Rayne 1.0                  |
+---------------------+----------------------------+
| **Declared in**     | RNShader.h                 |
+---------------------+----------------------------+
| **Companion guide** | :ref:`writing_shaders.rst` |
+---------------------+----------------------------+

Overview
========

The shader class encapsulates any number of shader programs that are compiled from the same source code, but with different variations to it. Raynes shader system allows, via the usage of defines and different shader types, one main shader source to be compiled in different variations. For example, one shader can be used to render objects with and without instancing and with and without lighting. This is done via an automated system which allows for a huge amount of flexibility and code re-use.

A concrete shader program is encapsulated via the :cpp:class:`ShaderProgram` class.

Differences to normal OpenGL
----------------------------

Shaders in Rayne are much more high-level concepts than shader programs in pure OpenGL. They provide a number of convenient methods that make them easy to work with. For example, you can add and remove additional defines to and from an existing shader at runtime and also use includes. Rayne allows for two kinds of includes, which are similar to the ones in C and C++: `#include ""` looks relative to the currently parsed shader file, whereas `#include <>` will look in the search paths defined in the :cpp:class`FileManager`.

Shader loading
--------------

There are two ways of loading shaders, either by pointing the shader to the shader files themselves, or by telling the shader the name of the shader files without extension. In the latter case, the shader will automatically load the right files using known file extensions. For example, if you load the shader file `foobar/myShader`, Rayne will try to load the following shader files:

* `foobar/myShader.fsh` as the fragment shader (this file must be present)
* `foobar/myShader.vsh` as the vertex shader (this file must be present)
* `foobar/myShader.gsh` as the geometry shader (this file is optional and is only loaded when support for geometry shaders is available)
* `foobar/myShader.tcsh` as the tessellation control shader (this file is optional and is only loaded when support for tessellation shader is available)
* `foobar/myShader.tesh` as the tessellation evaluation shader (this file is optional and is only loaded when support for tessellation shader is available)

Getting concrete shader programs
--------------------------------

The concrete shader programs are obtained by passing a :cpp:class:`ShaderLookup` to the :cpp:func:`GetProgramWithLookup() <Shader::GetProgramWithLookup>` method. If the shader program doesn't exist yet, it will be compiled on the fly, otherwise a cached version will be returned. The shader lookup is used to deduce the features that needs to be enabled when compiling the shader.

Tasks
=====

Construction
------------

* :cpp:func:`Shader() <Shader::Shader>`
* :cpp:func:`Shader(const std::string &shader) <Shader::Shader>`
* :cpp:func:`static WithFile(const std::string &shader) <Shader::WithFile>`

Altering shaders
----------------

* :cpp:func:`void Define(const std::string& define) <Shader::Define>`
* :cpp:func:`void Define(const std::string& define, const std::string& value) <Shader::Define>`
* :cpp:func:`void Define(const std::string& define, int32 value) <Shader::Define>`
* :cpp:func:`void Define(const std::string& define, float value) <Shader::Define>`
* :cpp:func:`void Undefine(const std::string& define) <Shader::Undefine>`
* :cpp:func:`void SetShaderForType(const std::string& path, ShaderType type) <Shader::SetShaderForType>`
* :cpp:func:`void SetShaderForType(File *file, ShaderType type) <Shader::SetShaderForType>`

Retrieving data
---------------

* :cpp:func:`GetProgramOfType(uint32 type) <Shader::GetProgramOfType>`
* :cpp:func:`GetProgramWithLookup(const ShaderLookup& lookup) <Shader::GetProgramWithLookup>`
* :cpp:func:`SupportsProgramOfType(uint32 type) <Shader::SupportsProgramOfType>`
* :cpp:func:`GetShaderSource(ShaderType type) <Shader::GetShaderSource>`
* :cpp:func:`std::string GetFileHash() const <Shader::GetFileHash>`

Class Methods
=============

.. class:: Shader

	.. function:: static Shader *WithFile(const std::string &shader)

		Returns the shader which uses the given file base name, either by creating it, or returning a cached version from the :cpp:class:`ResourceCoordinator`. If a new instance was created, it is added to the resource coordinator and subsequent calls of this method with the same argument will return the cached version.

Instance Methods
================

.. class:: Shader
	
	.. function:: Shader()

		Creates a new shader object without any shader sources attached to it. You must attach at least a vertex and fragment shader source before rendering with the shader.

	.. function:: Shader(const std::string &file)

		Creates a new shader object using the given file name as file base name to deduce shader files to automatically attach to the shader.

	.. function:: void Define(const std::string &define)

		Adds the given define to the shader

		.. note:: This will invalidate any previously compiled programs based on this shader

	.. function:: void Define(const std::string &define, const std::string &value)

		Adds the given define with the given value to the shader

		.. note:: This will invalidate any previously compiled programs based on this shader

	.. function:: void Define(const std::string &define, int32 value)

		Adds the given define with the given value to the shader

		.. note:: This will invalidate any previously compiled programs based on this shader

	.. function:: void Define(const std::string &define, float value)

		Adds the given define with the given value to the shader

		.. note:: This will invalidate any previously compiled programs based on this shader

	.. function:: void Undefine(const std::string &define)

		Removes the given define from the shader.

		.. note:: This will invalidate any previously compiled programs based on this shader

	.. function:: void SetShaderForType(const std::string& path, ShaderType type)

		Sets the source code of the given shader type to the contents of the file at the given path

		.. note:: This will invalidate any previously compiled programs based on this shader

	.. function:: void SetShaderForType(File *file, ShaderType type)

		Sets the source code of the given shader type to the contents of the given file

		.. note:: This will invalidate any previously compiled programs based on this shader

	.. function:: ShaderProgram *GetProgramOfType(ShaderProgram::Type type)

		Returns the shader program with the given type. Equivalent to calling `GetProgramWithLookup(ShaderLookup(type))`

		.. seealso:: :cpp:func:`Shader::GetProgramWithLookup`

	.. function:: ShaderProgram *GetProgramWithLookup(const ShaderLookup &lookup)

		Returns the shader program matching the given lookup, either by compiling it or saving a cached version. If the base shader source doesn't support shader programs with the given lookup type, the function will return nullptr.

	.. function:: bool SupportsProgramOfType(ShaderProgram::Type type)

		Returns true if the base shader source supports creating shader programs of the given type, otherwise false

	.. function:: const std::string &GetShaderSource(ShaderType type)

		Returns the source for the given shader. The shader source is unprocessed, as in, it doesn't have any of the additional defines added to it, however, all includes are resolved.

	.. function:: std::string GetFileHash() const

		Returns the file hash that identifies the shader. The structure and content of the hash may change in the future, so the returned format should not be depended on. In general, using this function is rarely useful and it should probably not be called.

Constants
=========

	.. type:: ShaderType

		* :code:`VertexShader` Vertex shader type
		* :code:`FragmentShader` Fragment shader type
		* :code:`GeometryShader` Geometry shader type
		* :code:`TessellationControlShader` Tessellation control shader type
		* :code:`TessellationEvaluationShader` Tessellation evaluation shader type
