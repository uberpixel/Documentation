.. _rbkinematic_controller.rst

***********************************
KinematicController class reference
***********************************

.. namespace:: RN
.. namespace:: bullet
.. class:: KinematicController

+-------------------+------------------------------+
| **Inherits from** | :cpp:class:`CollisionObject` |
+-------------------+------------------------------+
| **Availability**  | rayne-bullet                 |
+-------------------+------------------------------+
| **Declared in**   | RBKinematicController.h      |
+-------------------+------------------------------+
| **Namespace**     | bullet                       |
+-------------------+------------------------------+

Overview
========

TBA

Tasks
=====

Construction and Destruction
----------------------------

* :cpp:func:`KinematicController() <KinematicController::KinematicController>`
* :cpp:func:`~KinematicController() override <KinematicController::~KinematicController override>`

Getters and Setters
-------------------

* :cpp:func:`SetWalkDirection() <KinematicController::SetWalkDirection>`
* :cpp:func:`SetFallSpeed() <KinematicController::SetFallSpeed>`
* :cpp:func:`SetJumpSpeed() <KinematicController::SetJumpSpeed>`
* :cpp:func:`SetMaxJumpHeight() <KinematicController::SetMaxJumpHeight>`
* :cpp:func:`SetMaxSlope() <KinematicController::SetMaxSlope>`
* :cpp:func:`SetGravity() <KinematicController::SetGravity>`
* :cpp:func:`virtual GetBulletCollisionObject() <KinematicController::GetBulletCollisionObject>`

Actions
-------

* :cpp:func:`Update() override <KinematicController::Update override>`
* :cpp:func:`IsOnGround() <KinematicController::IsOnGround>`
* :cpp:func:`Jump() <KinematicController::Jump>`

Instance Methods
================

TBA
