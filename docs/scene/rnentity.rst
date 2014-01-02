.. _rnentity.rst:

**********************
Entity class reference
**********************

.. namespace:: RN
.. class:: Entity 

+---------------------+--------------------------------------+
|  **Inherits from**  | :cpp:class:`SceneNode`               |
+---------------------+--------------------------------------+
|   **Availability**  | Rayne 1.0                            |
+---------------------+--------------------------------------+
| **Declared in**     | RNEntity.h                           |
+---------------------+--------------------------------------+

Overview
========

The Entity class extends the SceneNode class to allow rendering of models, optionally also with a skeleton for animation. Entities usually make up the majority of the visible scene, because they take care of LOD and correct rendering of their model. A Entity without a model behaves exactly like a SceneNode.

Tasks
=====

Construction
------------

* :cpp:func:`Entity() <Entity::Entity>`
* :cpp:func:`Entity(Model *model) <Entity::Entity>`
* :cpp:func:`Entity(Model *model, const Vector3& position) <Entity::Entity>`

Modification
------------

* :cpp:func:`SetModel(Model *model) <Entity::SetModel>`
* :cpp:func:`SetSkeleton(class Skeleton *skeleton)<Entity::SetSkeleton>`
* :cpp:func:`GetModel() <Entity::GetModel>`
* :cpp:func:`GetSkeleton()<Entity::GetSkeleton>`

Instance Methods
================

.. class:: Entity
	
	.. function:: Entity()

		Designated constructor. Initializes the model and skeleton to nullptr

	.. function:: Entity(Model *model)

		Constructs the entity and initializes the model to the given model

	.. function:: Entity(Model *model, const Vector3& position)

		Constructs the entity at the given position and initializes the model to the given model

	.. function:: void SetModel(Model *model)

		Sets the model of the entity to the given model. This will also update the entities bounding volumes to the bounding volumes of the model. The model can be nullptr, which will just remove any previously set model.

	.. function:: void SetSkeleton(Skeleton *skeleton)

		Sets the skeleton of the entity to the given skeleton. The skeleton can be nullptr, which will just remove any previously set skeleton.

	.. function:: Model *GetModel()

		Returns the model of the entity

	.. function:: Skeleton *GetSkeleton()

		Returns the skeleton of the entity

