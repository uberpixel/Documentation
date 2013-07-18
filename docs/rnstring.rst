.. _rnstring.rst:

***************************
String class reference
***************************

.. namespace:: RN
.. class:: String : public Object

+---------------------+--------------------------------------+
|  **Inherits from**  |         :cpp:class:`Object`          |
+---------------------+--------------------------------------+
| **Availability**    | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | | RNString.h                         |
|                     | | RNUnicode.h                        |
+---------------------+--------------------------------------+
| **Companion guide** | :ref:`getting_started.rst`           |
+---------------------+--------------------------------------+
| **Sample code**     | :ref:`Example <getting_started.rst>` |
+---------------------+--------------------------------------+

Overview
========

Object implements the root class for most high level classes in Rayne.

Tasks
=====

Creating strings
----------------

* :cpp:func:`String <String::String>`
* :cpp:func:`WithFormat <String::WithFormat>`
* :cpp:func:`WithString <String::WithString>`
* :cpp:func:`WithBytes <String::WithBytes>`

Manipulating strings
--------------------

* :cpp:func:`Append() <String::Append>`
* :cpp:func:`Insert() <String::Insert>`
* :cpp:func:`DeleteCharacters() <String::DeleteCharacters>`
* :cpp:func:`ReplaceCharacters() <String::ReplaceCharacters>`
* :cpp:func:`ReplaceOccurrencesOfString() <String::ReplaceOccurrencesOfString>`

Comparing strings
-----------------

* :cpp:func:`RangeOfString() <String::RangeOfString>`
* :cpp:func:`Compare() <String::Compare>`

Accessing strings
-----------------

* :cpp:func:`Substring() <String::Substring>`
* :cpp:func:`CharacterAtIndex() <String::CharacterAtIndex>`
* :cpp:func:`Length() <String::Length>`
* :cpp:func:`BytesWithEncoding() <String::BytesWithEncoding>`
* :cpp:func:`UTF8String() <String::UTF8String>`

Class Methods
=============

.. class:: String

	.. function:: String()

	.. function:: String(const char *string, va_list args)

		Constructs a string using the given ASCII string and variable argument list. The ASCII string is parsed in a printf() style
		and the resulting string contains the formatted result.

		:param string: ASCII string with format specifiers
		:param args: List with arguments that matches the format specifiers of the string

	.. function:: String(const char *string, bool constant=false)

	.. function:: String(const char *string, size_t length, bool constant=false)

	.. function:: String(const void *bytes, Encoding encoding, bool constant=false)

	.. function:: String(const void *bytes, size_t length, Encoding encoding, bool constant=false)

	.. function:: String(const String *string)
	
	.. function:: static String *WithFormat(const char *string, ...)

	.. function:: static String *WithString(const char *string, bool constant=false)

	.. function:: static String *WithString(const char *string, size_t length, bool constant=false)

	.. function:: static String *WithBytes(const void *bytes, Encoding encoding, bool constant=false)

	.. function:: static String *WithBytes(const void *bytes, size_t length, Encoding encoding, bool constant=false)

Instance Methods
================

.. class:: String

	.. function:: void Append(const String *string)

		Appends the other string to the end of the receiver
