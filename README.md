## GeometRi
### Simple and lightweight computational geometry library for .Net

GeomtRi is a simple and lightweight 3D geometry library for .Net.
It is not one more 3D graphics library, its main job is manipulations with basic
geometrical primitives, such as point, line, plane, segment in 3D space:
translation and rotation operations, distance calculation, intersections,
orthogonal projections of one object into another, etc. The objects can be defined
in global or in one of the local coordinate systems and converted form one coordinate
system into another.

The library was build to be as simple and intuitive as posible. Users do not have to remember the reference coordinate
system of each object. The objects store the coordinate system they are defined in and all transformations
will be caried out implicitly when necessary.  

The main goal was simplisity and readability of the code, therefore speed and robustness was not a priority.
Global tolerance property is used for proximity checking, not an exact robust algorithms.

### Installation
Use NuGet to install library. Search for __GeometRi__ in NuGet package manager or type in the Package Manager Console:
```
Install-Package GeometRi
```

### Classes

* __Point3d__ and __Vector3d__ are two base classes, representing points and vectors in 3D space.
Objects of type Point3d or Vector3d can be defined in global or in local coordinate systems.

* __Line3d__, __Ray3d__, __Segment3d__, __Plane3d__, __Circle3d__, __Sphere__ and __Triangle__
are compound classes, which are defined in terms of points and vectors.

* __Coord3d__ and __Matrix3d__ are auxiliary classes.

* __GeometRi3d__ is an abstract class, which defines some common functionality, for example global tolerance property (GeometRi3d.Tolerance)
used in proximity operations by other classes. Implements tolerance based equality methods: AlmostEqual(double, double), NotEqual(double,double),
Greater(double, double) and Smaller(double, double).

#### Some common methods implemented by other classess (when applicable)

* __Translate(Vector3d)__ - translate object by given vector.
* __Rotate(Matrix3d, [Point3d])__ - rotate object by given rotation matrix (optionally rotate around given point).
* __ReflectIn(obj)__ - reflect object in given point, line or plane.
* __DistanceTo(obj)__ - distance to other object (point, line or plane).
* __ProjectionTo(obj)__ - orthogonal projection of one object to another.
* __IntersectionWith(obj)__ - intersection of two objects.
* __AngleTo(obj)__ - angle between two objects (radians).
* __AngleToDeg(obj)__ - angle between two objects (degrees).
* __Clone()__ - creates copy of the object.
* __ConvertTo(coord)__ - convers point or vector to local cordinate system.
* __ConvertToGlobal()__ - convert point or vector to global coordinate system.

#### Point3d

One of the base classes, can be constructed by three double numbers (X, Y and Z) or from double array.
Each constructor has optional parameter 'coord' for local coordinate system in which point will be defined.
By default all points are defined in global coordinate system.
##### Properties
* __X__ - X coordinate in reference coordinate system
* __Y__ - Y coordinate in reference coordinate system
* __Z__ - Z coordinate in reference coordinate system
* __Coord__ - reference coordinate system
* __ToVector__ - radius vector of point
##### Methods
* __Clone__ - deep copy of object
* __ConvertTo__ - convert point to local coordinate system
* __ConvertToGlobal__ - convert point to global coordinate system
* __Add__ - add two points
* __Subtract__ - subtract one point from other
* __Scale__ - scale point by given number
* __DistanceTo__ - shortest distance from point to point, line, plane, ray or segment
* __ProjectionTo__ - orthogonal projection of point to line, plane or sphere
* __BelongsTo__ - check if point belongs to line, ray, segment, plane, circle, ellipse or sphere surface
* __IsInside__ - check if point is inside circle or sphere
* __Translate__ - translate point by vector
* __Rotate__ - rotate point around origin or other point
* __Reflect__ - reflect point in point, line or plane
* __Equals__ - check if two points are equals
* __ToString__ - string representation of point in global or local coordinate system
##### Static methods
* __CollinearPoints__ - check if three points are collinear
##### Overloaded operators
* __+__ - add two points
* __-__ - subtract one point from other
* __-__ - unary operator
* __*__ - scale point by number
* __/__ - scale point by number
* __=__ - equality check
* __<>__ - unequality check

#### Vector3d

Second base class, representing vector in 3D space. Constructed by three components (X, Y and Z) or from double array
(with optional 'coord' parameter for local cordinate system). Additionally, can be constructed by point,
representing radius vector of that point, or by two points, representing vector from first point to another. In this cases
the vector will be defined in the same coordinate system as the first operand.
##### Properties
* __X__ - X component in reference coordinate system
* __Y__ - Y component in reference coordinate system
* __Z__ - Z component in reference coordinate system
* __Coord__ - reference coordinate system
* __Norm__ - Norm of a vector
* __ToPoint__ - point, represented by vector starting in origin
* __OrthogonalVector__ - return arbitrary vector, orthogonal to the current vector
##### Methods
* __Clone__ - deep copy of object
* __ConvertTo__ - convert vector to local coordinate system
* __ConvertToGlobal__ - convert vector to global coordinate system
* __Normalize__ - normalize the current vector
* __Normalized__ - return normalized vector
* __IsParallelTo__ - check if two vectors are parallel
* __IsNotParallelTo__ - check if two vectors are NOT parallel
* __IsOrthogonalTo__ - check if two vectors are orthogonal
* __Add__ - overloaded, add number or vector
* __Subtract__ - oveloaded, subtract number or vector
* __Mult__ - overloaded, multiply by number or vector
* __Dot__ - dot product of two vectors
* __AngleTo__ - angle between vector and other vector, line, plane, ray or segment
* __AngleToDeg__ - angle between vector and other vector, line, plane, ray or segment (in degrees)
* __ProjectionTo__ - return projection of the current vector to the second vector
* __Rotate__ - rotate vector around origin
* __Reflect__ - reflect vector in point, line or plane
* __Equals__ - check if two vectors are equals
* __ToString__ - string representation of vector in global or local coordinate system

#### Line3d 

Represent infinite line  in 3D space and is defined by any point lying on the line and a direction vector.
##### Properties
* __Point__ - base point of the line
* __Direction__ - direction vector of the line
##### Methods
* __Clone__ - deep copy of object
* __DistanceTo__ - shortest distance to point, line, ray or segment
* __PerpendicularTo__ - point on the perpendicular to the second line
* __IntersectionWith__ - intersection of line with plane or sphere
* __ProjectionTo__ - orthogonal projection of a line to the plane
* __AngleTo__ - angle between line and other line or plane
* __AngleToDeg__ - angle between line and other line or plane (in degrees)
* __Translate__ - translate line by vector
* __Rotate__ - rotate line around origin or other point
* __Reflect__ - reflect line in point, line or plane
* __Equals__ - check if two lines are equals
* __ToString__ - string representation of line in global or local coordinate system

#### Ray 3d

Represent ray in 3D space and is defined by starting point and direction vector.

#### Plane3d

Defined by arbutrary point on the plane and a normal vector. 
Optionally can be defined by coefficients in general equation of plane (Ax + By + Cz + D = 0), by three points
or by point and two vectors in the plane.

#### Sphere

Defines a sphere in 3D space. Implements intersection with line, plane and other sphere methods, projection to line and plane, as well as
common translation, rotation and reflection methods.

#### Circle3d

Defines a circle in 3D space. Implements common translation, rotation and reflection methods.

#### Triangle

Defines a triangle n 3D space. Implements common translation, rotation and reflection methods. Calculates most of the standard
triangle properties: bisectors, meadians, altitudes, incenter, circumcenter, centroid, orthocenter, etc.

#### Coord3d

Class representing orthogonal cartesian 3D coordinate system. Defined by an origin point and transformation matrix
(three orthogonal unit vectors stored in row format). One global coordinate system (Coord3d.GlobalCS) is defined by default,
any number of local coordinate systems can be defined by users.