.. _rndefines.rst:

********************
Data types reference
********************

.. namespace:: RN

+-----------------+----------------+
| **Declared in** | | RNCostants.h |
|                 | | RNBase.h     |
+-----------------+----------------+

Overview
========

This document describes the fundamental data types found in Rayne.

Data Types
==========

.. type:: int8

	Type capable of holding 1 signed byte

.. type:: int16

	Type capable of holding 2 signed bytes

.. type:: int32

	Type capable of holding 4 signed bytes

.. type:: int64

	Type capable of holding 8 signed bytes

.. type:: uint8

	Type capable of holding 1 unsigned byte

.. type:: uint16

	Type capable of holding 2 unsigned bytes

.. type:: uint32

	Type capable of holding 4 unsigned bytes

.. type:: uint64

	Type capable of holding 8 unsigned bytes

.. type:: machine_hash

	Type capable of holding a hash value fitting for the current architecture.
	This type is 4 bytes on 32 bit machines, and 8 bytes on 64 bit machines.

.. type:: FrameID

	An unsigned integer that can hold the ID of the current rendering frame.
	Frames are always in sequential order, so the next frame is always the ID of the current frame + 1

	.. seealso::

		:cpp:func:`Kernel::CurrentFrame`

.. class:: Range

	The Range class represents a range of indices starting at :cpp:member:`origin` and a length of :cpp:member:`length`.
	It is used for example by the :cpp:class:`String class <String>` to represent ranges of substrings within the string.
	
	.. function:: Range()

		Default constructor. Doesn't initialize offset or length

	.. function:: Range(size_t origin, size_t length)

		Constructs a range using the given origin and length

	.. function:: size_t End() const

		Returns the last index covered by the range. This is the same as :code:`origin + length`

	.. function:: bool Contains(const Range& other)

		Returns true if the range completely contains the other range

	.. function:: bool Overlaps(const Range& other)

		Returns true if the range overlaps with the other range

	.. member:: size_t origin

		The origin, or offset, of the range. 
		Can be :cpp:type:`k::NotFound` to signal an invalid range.

	.. member:: size_t length

		The length of the range

.. class:: Singleton<T>
	
	Provides a base class to implement singletons. The class provides a getter to access the shared instance of
	the singleton, and if it doesn't exist yet, the singleton is constructed using its default constructor.

	.. function:: static T *SharedInstance()

		Returns the shared instance of the singleton. If it doesn't exist yet, an instance will be constructed using the default constructor.

		.. note::
			| This method will always return a valid pointer 
			| This method is thread safe 

	.. admonition:: Example

		.. code::

			class MyClass : public Singleton<MyClass>
			{};

			// ...

			MyClass *instance = MyClass::SharedInstance();
	
.. class:: NonConstructingSingleton<T>
	
	Similar to :cpp:class:`Singleton\<T>`, but isn't automatically constructed when the shared instance
	is requested but not found. The first instance constructed is used the shared instance, and attempting to
	construct further instances will raise an assertion.

	.. function:: static T *SharedInstance()

		Returns the shared instance of the singleton, or nullptr if there is none

.. type:: enum ComparisonResult

	Enum used to signal the result of an comparison of two values.

	* :code:`LessThan = -1` Signals that the left side is less than the right side
	* :code:`EqualTo = 0` Signals that both sides are equal
	* :code:`GreaterThan = 1` Signals that the left side is greater than the right side

