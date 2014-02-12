.. _rndefines.rst:

*****************
Defines reference
*****************

.. namespace:: RN

+-----------------+-------------+
| **Declared in** | RNDefines.h |
+-----------------+-------------+

Overview
========

This documents describes the global preprocessor defines found in Rayne, which can be used to conditionally compile for different targets and architectures. All defines are always defines, the only difference is that they are defined a `1` when active and as `0` when inactive.

.. admonition:: Example
	
	.. code:: cpp

		#if RN_PLATFORM_32BIT
			// 32 bit code here
		#endif

		#if RN_PLATFORM_64BIT
			// 64 bit code here
		#endif


Defines
=======

.. c:macro:: RN_PLATFORM_MAC_OS

	Defined as 1 when compiling for OS X, otherwise 0

.. c:macro:: RN_PLATFORM_WINDOWS

	Defined as 1 when compiling for Windows, otherwise 0

.. c:macro:: RN_PLATFORM_LINUX

	Defined as 1 when compiling for Linux, otherwise 0

.. c:macro:: RN_PLATFORM_INTEL

	Defined as 1 when compiling for IA32 or AMD64 CPUs, otherwise 0

.. c:macro:: RN_PLATFORM_LINUX

	Defined as 1 when compiling for ARM based CPUs, otherwise 0

.. c:macro:: RN_PLATFORM_32BIT

	Defined as 1 when compiling for 32 bit architectures, otherwise 0

.. c:macro:: RN_PLATFORM_64BIT

	Defined as 1 when compiling for 64 bit architectures, otherwise 0

.. c:macro:: RN_TARGET_OPENGL

	Defined as 1 when compiling for OpenGL

.. c:macro:: RN_TARGET_OPENGLES

	Defined as 1 when compiling for OpenGL ES

.. c:macro:: RN_TARGET_CXX_NOXCEPT

	Defined as 1 when the compiler supports the C++11 noexcept qualifier

.. c:macro:: RN_TARGET_CXX_CONSTEXPR

	Defined as 1 when the compiler supports the C++11 constexpr qualifier

.. c:macro:: RN_BUILD_DEBUG

	Defined as 1 when compiling as debug build

.. c:macro:: RN_BUILD_RELEASE

	Defined as 1 when compiling as release build
