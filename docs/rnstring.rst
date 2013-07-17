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

Instance Methods
================

.. function:: String::String(const char *string, va_list args)

	Constructs a string using the given ASCII string and variable argument list. The ASCII string is parsed in a printf() style
	and the resulting string contains the formatted result.

	:param string: ASCII string with format specifiers
	:param args: List with arguments that matches the format specifiers of the string