.. _rnsettings.rst:

************************
Settings class reference
************************

.. namespace:: RN
.. class:: Settings

+-------------------+-------------------------------------------------------+
| **Inherits from** | :cpp:class:`ISingleton\<Settings\> <ISingleton\<T\>>` |
+-------------------+-------------------------------------------------------+
| **Availability**  | Rayne 1.0                                             |
+-------------------+-------------------------------------------------------+
| **Declared in**   | RNSettings.h                                          |
+-------------------+-------------------------------------------------------+

Overview
========

The settings class provides access to user defined settings that stay valid across application runs. It can serialize any valid JSON type, ie :cpp:class:`Array`, :cpp:class:`Dictionary`, :cpp:class:`Number`, :cpp:class:`String` and :cpp:class:`Null`. The initial values of the settings come from the settings.json within the resource bundle of the application, after the initial run, the settings are stored on the users disk in the following location:

* Mac OS X: `~/Library/Application Support/GAME/settings.json`
* Windows: `$DOCUMENTS\GAME\settings.json`
* Linux: `~/.GAME/settings.json`

There is no need to manually flush the settings, as this is done automatically in the background in periodic intervals, or when catching an unhandled exception or on a normal engine shutdown.

Additionally, the settings class also provides access to the manifest.json, albeit only reading access.

Tasks
=====

Reading and writing settings
----------------------------

* :cpp:func:`GetBoolForKey(String *key, bool defaultValue = false) <Settings::GetBoolForKey>`
* :cpp:func:`GetFloatForKey(String *key, float defaultValue = 0.0f) <Settings::GetFloatForKey>`
* :cpp:func:`GetInt32ForKey(String *key, int32 defaultValue = 0) <Settings::GetInt32ForKey>`
* :cpp:func:`GetUint32ForKey(String *key, uint32 defaultValue = 0) <Settings::GetUint32ForKey>`
* :cpp:func:`SetBoolForKey(String *key, bool value) <Settings::SetBoolForKey>`
* :cpp:func:`SetFloatForKey(String *key, float value) <Settings::SetFloatForKey>`
* :cpp:func:`SetInt32ForKey(String *key, int32 value) <Settings::SetInt32ForKey>`
* :cpp:func:`SetUint32ForKey(String *key, uint32 value) <Settings::SetUint32ForKey>`
* :cpp:func:`GetObjectForKey(String *key) <Settings::GetObjectForKey>`
* :cpp:func:`SetObjectForKey(Object *object, String *key) <Settings::SetObjectForKey>`
* :cpp:func:`RemoveObjectForKey(String *key) <Settings::RemoveObjectForKey>`

Reading manifest.json data
--------------------------

* :cpp:func:`GetManifestObjectForKey(String *key) <Settings::GetManifestObjectForKey>`

Instance Methods
================

.. class:: Settings

	.. function:: bool GetBoolForKey(String *key, bool defaultValue = false)

		Returns the boolean value associated with the given key, or the default value if no object exists with the key. Throws a downcast exception if the object stored isn't of type Number.

	.. function:: float GetFloatForKey(String *key, float defaultValue = 0.0f)

		Returns the floating point value associated with the given key, or the default value if no object exists with the key. Throws a downcast exception if the object stored isn't of type Number.

	.. function:: int32 GetInt32ForKey(String *key, int32 defaultValue = 0)

		Returns the signed 32 bit integer value associated with the given key, or the default value if no object exists with the key. Throws a downcast exception if the object stored isn't of type Number.

	.. function:: uint32 GetUint32ForKey(String *key, uint32 defaultValue = 0)

		Returns the unsigned 32 bit integer value associated with the given key, or the default value if no object exists with the key. Throws a downcast exception if the object stored isn't of type Number.

	.. function:: void SetBoolForKey(String *key, bool value)

		Associates the given boolean value with the given key in the settings

	.. function:: void SetFloatForKey(String *key, float value)

		Associates the given floating point value with the given key in the settings

	.. function:: void SetInt32ForKey(String *key, int32 value)

		Associates the given 32 bit signed integer value with the given key in the settings

	.. function:: void SetUint32ForKey(String *key, uint32 value)

		Associates the given 32 bit unsigned integer value with the given key in the settings

	.. function:: T *GetObjectForKey(String *key)

		Returns the object associated with the given settings key, or nullptr if no object with the given key exists. Throws a downcast exception if the object isn't of the expected type T.

		The full signature for the method is:

		.. code:: cpp

			template<class T=Object>
			T *GetObjectForKey(String *key)

	.. function:: void SetObjectForKey(Object *object, String *key)

		Associates the given object with the given key. Throws an invalid argument exception if the object can't be serialized into a valid JSON object.

	.. function:: void RemoveObjectForKey(String *key)

		Removes any value associated with the given key.

	.. function:: T *GetManifestObjectForKey(String *key)

		Similar to the `GetObjectForKey` method, but read from the manifest.json

		The full signature for the method is:

		.. code:: cpp

			template<class T=Object>
			T *GetManifestObjectForKey(String *key)

