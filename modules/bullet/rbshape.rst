.. _rbshape.rst

**********************
Shape class references
**********************

.. namespace:: RN
.. namespace:: bullet
.. class:: Shape

+-------------------+---------------------+
| **Inherits from** | :cpp:class:`Object` |
+-------------------+---------------------+
| **Availability**  | rayne-bullet        |
+-------------------+---------------------+
| **Declared in**   | RBShape.h           |
+-------------------+---------------------+
| **Namespace**     | bullet              |
+-------------------+---------------------+

Overview
========

TBA

Tasks
=====

Construction and Destruction
----------------------------

* :cpp:func:`Shape() <Shape::Shape>`

Getters and Setters
-------------------

* :cpp:func:`virtual CalculateLocalInertia() <Shape::CalculateLocalInertia>`
* :cpp:func:`SetScale() <Shape::SetScale>`
* :cpp:func:`GetBulletShape() <Shape::GetBulletShape>`

Instance Methods
================

.. class:: Shape

	.. function:: Shape(btCollisionShape *shape)

		Default constructor.

	.. function:: Vector3 CalculateLocalInertia(float mass)

		Get the shape's resistance to change.

	.. function:: void SetScale(const Vector3 &scale)

		Manipulate the scale of the shape with a vector.

	.. function:: btCollisionShape *GetBulletShape() const

		Get the raw bullet shape for advanced usage.

Subclasses
==========

These classes are all subclasses of :cpp:class:`Shape`, and what you will probably be actually using instead of a raw shape. They are all in the same header, namespace, and module. The only thing these classes have in addition to the previous class are specialized constructors.

SphereShape
-----------

.. class:: SphereShape

	A shape that is also a sphere.

	.. function:: SphereShape(float radius)

		Default constructor.

	.. function:: static SphereShape *WithRadius(float radius)

		Constructor using a static method.

BoxShape
--------

.. class:: BoxShape

	A shape that is also a box.

	.. function:: BoxShape(const Vector3 &halfExtents)

		Default constructor. The 3 components of halfEntents are half the sizes of the box's length, width, and height.

	.. function:: static BoxShape *WithHalfExtents(const Vector3& halfExtents)

		Constructor using a static method.

CylinderShape
-------------

.. class:: CylinderShape

	A shape that is also a cylinder.

	.. function:: CylinderShape(const Vector3 &halfExtents)

		Default constructor. See :cpp:class:`BoxShape` for more information about half extents.

	.. function:: static CylinderShape *WithHalfExtents(const Vector3 &halfExtents)

		Constructor using a static method.

CapsuleShape
------------

.. class:: CapsuleShape

	A shape that is easy to swallow. Maybe useful as a character placeholder.

	.. function:: CapsuleShape(float radius, float height)

		Default constructor.

	.. function:: static CapsuleShape *WithRadius(float radius, float height)

		Constructor using a static method.

TriangleMeshShape
-----------------

.. class:: TriangleMeshShape

	Generates a shape from a model, or at least one mesh.

	.. function:: TriangleMeshShape(Model *model)

		Generate a shape from a model.

	.. function:: TriangleMeshShape(Mesh *mesh)

		Generate a shape from a single mesh.

	.. function:: TriangleMeshShape(const Array *meshes)

		Generate a shape from an array of meshes.

	.. function:: static TriangleMeshShape *WithModel(Model *model)

		Constructor using a static method. Generates from a model.

MultiSphereShape
----------------

.. class:: MultiSphereShape

	A convex shape defined by spheres. Useful for representing beveled boxes or other shapes without sharp corners. Also since the spheres can be independently scaled in each of the 3 dimensions, a :cpp:class:`MultiSphereShape` containing just one sphere can be useful to create ellipsoids (squashed spheres), which is not possible with :cpp:class:`SphereShape`.

	.. function:: MultiSphereShape(const Vector3 *positions, float *radii, int count)

		Default constructor. Takes in a c-array of :cpp:class:`Vector3` for positions, another of floats for roadii, and the count.

	.. function:: static MultiSphereShape *WithHeight(float height, float width)

		Constructor using a static method. 

StaticPlaneShape
----------------

.. class:: StaticPlaneShape

	A static plane that is solid to infinity on one side. Several of these can be used to confine a convex space in a manner that completely prevents tunneling to the outside.

	.. function:: StaticPlaneShape(const Vector3 &normal, float constant)

		Default constructor. The normal is directly perpendicular to the ground.

	.. function:: static StaticPlaneShape *WithNormal(const Vector3 &normal, float constant)

		Constructor using a static method.
