.. _anatomy.rst:

**********************************
The anatomy of a Rayne application
**********************************

At its core, each application build against Rayne has a similar structure and known layout. This document describes the basic layout of an application on disk as well as the basic layout code-wise. It's not a getting started guide but a reference for the basics layout of an Rayne application.


It's JSON all the way down
==========================

Rayne uses JSON as file format of choice. JSON has numerous advantages over XML, both in terms of readability and parser speed. JSON can also be natively serialized and deserialized via the :cpp:class:`JSONSerialization` class. Because of this, the core settings files used by Rayne are in JSON, which also means that they are easily editable by the user. If you require that the core files are unaltered, you can use the :cpp:class:`stl::sha2_context` class to get a quick finger print off of a file.

Manifest.json
-------------

The manifest.json is one of the *required* files for a Rayne application. It's meant to be an immutable manifest of your application, which tells Rayne which modules to load, how your application is named and a variety of other things. The manifest.json must be found in the root of one the registered search paths.

Within the manifest.json, there are two mandatory key/value pairs that must be defined, otherwise the engine will refuse to start. The first one is `RNApplication`, which is the key to a string denoting the name of your application. The second key is `RNUIStyle` which is another string for the `json` file describing the UI style.

Here is a list of all keys:

* `RNApplication` *mandatory*, the name of your application.
* `RNUIStyle` *mandatory*, the path to the root UI json file
* `RNModules` an array of strings with paths to modules that Rayne should load on startup



.. admonition:: Example

	.. code:: json

		{
			"RNApplication": "Test Game",
			"RNUIStyle": "ui/rn_uistyle.json",
			"RNModules": [
				"modules/librayne-assimp"
			]
		}

Settings.json
-------------

Though not mandatory, the settings.json allows shipping a default set of settings with your app. The settings.json will be copied into the save directory upon the first start, which then takes precedence from there on. While the format of the settings.json isn't mandated by Rayne, there are some keys that you can use that Rayne will pick up on.

Settings can be altered using the :cpp:class:`Settings` class.

* `RNGammaCorrection` boolean value that allows triggering of gamma correction. This should be set to `true` for best visual quality across displays
* `RNScreen` an object with "width" and "height" attributes, which are used for the initial resolution on startup
* `RNOpenGLRenderer` a string used to force a certain OpenGL renderer. Possible values are "3.2" and "4.1"


.. admonition:: Example

	.. code:: json

		{
			"RNGammaCorrection": true,
			"RNScreen": {
				"width": 1200,
				"height": 720,
				"fullscren": true
			}
		}

The Application class
=====================

Another mandatory part of Rayne is a custom :cpp:class:`Application` subclass. This mast be passed to the constructor of the :cpp:class:`Kernel` class, and it's used by the engine to communicate events back to the application.

Default files
=============

Rayne ships with a folder called `Engine Resources`, which contains required default files by the engine. Amongst others, it contains the default UI definition, the default shaders and some default textures. Unless you are providing own replacement files, the `Engine Resources` folder must be registered as a search path with the engine. Consequently, when shipping an application, this folder, or at least the required parts of it, should be shipped as well
