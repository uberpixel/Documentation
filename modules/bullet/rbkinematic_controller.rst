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
* :cpp:func:`~KinematicController() override <KinematicController::~KinematicController>`

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

* :cpp:func:`Update() override <KinematicController::Update>`
* :cpp:func:`IsOnGround() <KinematicController::IsOnGround>`
* :cpp:func:`Jump() <KinematicController::Jump>`

Instance Methods
================

.. class:: KinematicController

	.. function:: KinematicController(Shape *shape, float stepHeight)

		Default constructor.

	.. function:: ~KinematicController() override

		Default destructor.

	.. function:: void SetWalkDirection(const Vector3 &direction)

		Set the direction for the player to walk.

	.. function:: void SetFallSpeed(float speed)

		Set the speed at which the player falls.

	.. function:: void SetJumpSpeed(float speed)

		Set the speed that the player jumps at.

	.. function:: void SetMaxJumpHeight(float maxHeight)

		Set the maximum height the player can approach.

	.. function:: void SetMaxSlope(float maxSlope)

		Set the maximum steepness the player can walk up in.

	.. function:: void SetGravity(float gravity)

		Set the player's personal gravity.

	.. function:: void Update(float delta) override

		Update the player in the world.

	.. function:: bool IsOnGround()
			
		Check if the player is touching the ground.

	.. function:: void Jump()

		Jump!

	.. function:: btCollisionObject *GetBulletCollisionObject()

		Get the raw bullet object for advanced usage.
