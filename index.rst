
*******************
Rayne Documentation
*******************

Hi and welcome to the Rayne documentation. This conglomerate of documents provide you with everything you need to know to work with Rayne as effectively as possible. If you are new to Rayne, you probably want to start with the documents found in the `Getting to love Rayne`_ section. If you stumbled upon this documentation by accident and have no idea what Rayne is, Rayne is a fast, multi-platform game engine written in C++. Intrigued? Learn more about it `here <http://rayne3d.com>`_.

.. note:: Rayne is still very much in development, and the API is subject to change! This documentation is by no means complete; it only covers a very basic set of the API. Please read it anyways, and if you can, provide us with feedback at support@rayne3d.com! In addition, if you would like to provide us with feedback, the source for these docs is on `github <http://github.com/uberpixel/documentation>`_.

Getting to love Rayne
=====================

New to Rayne? Don't worry, we've got you covered! In this section, you will learn how to work with this documentation, how Rayne is structured and everything else you need to know to get going!

.. toctree::
	:maxdepth: 1
	
	love/how_to_read.rst
	love/naming.rst
	love/concepts.rst

Guides
======

.. toctree::
	:maxdepth: 1
	
	guides/anatomy.rst
	guides/modules.rst

API Reference
=============

Core
----
.. toctree::
	:maxdepth: 1

	docs/core/rntypes.rst
	docs/core/rndefines.rst
	docs/core/rnkernel.rst
	docs/core/rnapplication.rst
	docs/core/rnmemory.rst
	docs/core/rnsettings.rst

Math
----
.. toctree::
	:maxdepth: 1
	
	docs/math/rnconstants.rst
	docs/math/rnmath.rst
	docs/math/rnvector2.rst
	docs/math/rnvector3.rst
	docs/math/rnvector4.rst
	docs/math/rnmatrix.rst
	docs/math/rnquaternion.rst
	docs/math/rncolor.rst
	docs/math/rnplane.rst
	docs/math/rnsphere.rst
	docs/math/rnaabb.rst

Objects
-------
.. toctree::
	:maxdepth: 1
	
	docs/objects/rnobject.rst

Scene
-----
.. toctree::
	:maxdepth: 1
	
	docs/scene/rnworld.rst
	docs/scene/rnworldattachment.rst
	docs/scene/rnworldcoordinator.rst
	docs/scene/rnscenenode.rst
	docs/scene/rnentity.rst
	docs/scene/rncamera.rst
	docs/scene/rnlight.rst
	docs/scene/rnbillboard.rst

Rendering
---------
.. toctree::
	:maxdepth: 1

	docs/rendering/rnmaterial.rst
	docs/rendering/rnshader.rst
	docs/rendering/rnshaderprogram.rst
	docs/rendering/rnlightmanager.rst

Assets
------
.. toctree::
	:maxdepth: 1

	docs/assets/rnresourcecoordinator.rst
	docs/assets/rnresourceloader.rst

System
------
.. toctree::
	:maxdepth: 1

	docs/system/rnthread.rst
	docs/system/rnwindow.rst
	docs/system/rnwindowconfiguration.rst
	docs/system/rnscreen.rst

Misc
----
.. toctree::
	:maxdepth: 1
	
	docs/misc/rnsyncable.rst
	docs/misc/rnsyncpoint.rst
	docs/misc/rnringbuffer.rst
	docs/misc/rnlockfreeringbuffer.rst
	docs/misc/rnthreadlocalstorage.rst

Modules
=======

Rayne has an advanced module loading system that can greatly extend Rayne's feature-set. Does your game need physics, advanced artificial intelligence, more file formats, or audio? These can make your life *much* easier. Just follow the instructions stated `here <guides/modules.html>`_.

Bullet Physics
--------------
.. toctree::
	:maxdepth: 1

	modules/bullet/rbcollision_object.rst
	modules/bullet/rbkinematic_controller.rst
	modules/bullet/rbphysics_material.rst
	modules/bullet/rbphysics_world.rst
	modules/bullet/rbrigid_body.rst
	modules/bullet/rbshape.rst

Assimp Loader
-------------
.. toctree::
	:maxdepth: 1

	modules/assimp/raresource_loader_assimp.rst

OpenAL Audio
------------
.. toctree::
	:maxdepth: 1

	modules/openal/ralaudio_listener.rst
	modules/openal/ralaudio_resource_attachment.rst
	modules/openal/ralaudio_source.rst
	modules/openal/ralaudio_world.rst

OGG Loader
----------
.. toctree::
	:maxdepth: 1

	modules/ogg/roggresource_loader.rst

Misc
====
.. toctree::
	:maxdepth: 1

	misc/licensing.rst
	misc/thanks.rst


Indices and tables
==================

* :ref:`genindex`
* :ref:`search`

