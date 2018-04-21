# GeometRi
## Simple and lightweight computational geometry library for .Net

### This version is obsolete. Please use C# version of the library: [GeometRi.CSharp](https://github.com/RiSearcher/GeometRi.CSharp)

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

## Installation
Use NuGet to install library. Search for __GeometRi__ in NuGet package manager or type in the Package Manager Console:
```
Install-Package GeometRi
```

## Classes

* __Point3d__ and __Vector3d__ are two base classes, representing points and vectors in 3D space.
Objects of type Point3d or Vector3d can be defined in global or in local coordinate systems.

* __Line3d__, __Ray3d__, __Segment3d__, __Plane3d__, __Circle3d__, __Sphere__, __Ellipse__ and __Triangle__
are compound classes, which are defined in terms of points and vectors.

* __Coord3d__ and __Matrix3d__ are auxiliary classes.

* __GeometRi3d__ is an abstract class, which defines some common functionality, for example global tolerance property (GeometRi3d.Tolerance)
used in proximity operations by other classes. Implements tolerance based equality methods: AlmostEqual(double, double), NotEqual(double,double),
Greater(double, double) and Smaller(double, double).

## Point3d

One of the base classes, can be constructed by three double numbers (X, Y and Z) or from double array.
Each constructor has optional parameter 'coord' for local coordinate system in which point will be defined.
By default all points are defined in global coordinate system.
### Properties
* __X__ - X coordinate in reference coordinate system
* __Y__ - Y coordinate in reference coordinate system
* __Z__ - Z coordinate in reference coordinate system
* __Coord__ - reference coordinate system
* __ToVector__ - radius vector of point
### Methods
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
### Static methods
* __CollinearPoints__ - check if three points are collinear
### Overloaded operators
* __+__ - add two points
* __-__ - subtract one point from other
* __-__ - unary operator
* __*__ - scale point by number
* __/__ - scale point by number
* __=__ - equality check
* __<>__ - unequality check

## Vector3d

Second base class, representing vector in 3D space. Constructed by three components (X, Y and Z) or from double array
(with optional 'coord' parameter for local cordinate system). Additionally, can be constructed by point,
representing radius vector of that point, or by two points, representing vector from first point to another. In this cases
the vector will be defined in the same coordinate system as the first operand.
### Properties
* __X__ - X component in reference coordinate system
* __Y__ - Y component in reference coordinate system
* __Z__ - Z component in reference coordinate system
* __Coord__ - reference coordinate system
* __Norm__ - Norm of a vector
* __ToPoint__ - point, represented by vector starting in origin
* __OrthogonalVector__ - return arbitrary vector, orthogonal to the current vector
### Methods
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

## Line3d 

Represent infinite line  in 3D space and is defined by any point lying on the line and a direction vector.
### Properties
* __Point__ - base point of the line
* __Direction__ - direction vector of the line
### Methods
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

## Ray3d

Represent ray in 3D space and is defined by starting point and direction vector.
### Properties
* __Point__ - base point of the ray
* __Direction__ - direction vector of the ray
* __ToLine__ - convert ray to line
### Methods
* __Clone__ - deep copy of object
* __DistanceTo__ - shortest distance to point, line, segment or other ray
* __PerpendicularTo__ - point on the perpendicular to the line
* __IntersectionWith__ - intersection of ray with plane
* __ProjectionTo__ - orthogonal projection of ray to the plane
* __AngleTo__ - angle between ray and plane
* __AngleToDeg__ - angle between ray and plane (in degrees)
* __Translate__ - translate ray by vector
* __Rotate__ - rotate ray around origin or other point
* __Reflect__ - reflect ray in point, line or plane
* __Equals__ - check if two rays are equals
* __ToString__ - string representation of ray in global or local coordinate system

## Segment3d

Represent a line segment in 3D space and is defined by two points.
### Properties
* __P1__ - first point of the segment
* __P2__ - second point of the segment
* __Length__ - length of the segment
* __ToVector__ - convert segment to vector
* __ToRay__ - convert segment to ray
* __ToLine__ - convert segment to line
### Methods
* __Clone__ - deep copy of object
* __DistanceTo__ - shortest distance to point, line, ray, plane or other segment
* __IntersectionWith__ - intersection of segment with plane
* __ProjectionTo__ - orthogonal projection of segment to the line or plane
* __AngleTo__ - angle between segment and plane
* __AngleToDeg__ - angle between segment and plane (in degrees)
* __Translate__ - translate segment by vector
* __Rotate__ - rotate segment around origin or other point
* __Reflect__ - reflect segment in point, line or plane
* __Equals__ - check if two segments are equals
* __ToString__ - string representation of serment in global or local coordinate system

## Plane3d

Defined by arbutrary point on the plane and a normal vector. 
Optionally can be defined by coefficients in general equation of plane (Ax + By + Cz + D = 0), by three points
or by point and two vectors in the plane.
### Properties
* __Point__ - point on the plane
* __Normal__ - normal vector of the plane
* __A/B/C/D__ - coefficients A, B, C and D in the general plane equation
### Methods
* __Clone__ - deep copy of object
* __SetCoord__ - set reference coordinate system for general plane equation
* __IntersectionWith__ - intersection of plane with line, plane, sphere, circle or two other planes
* __AngleTo__ - angle between plane and vector, line or plane
* __AngleToDeg__ - angle between plane and vector, line or plane (in degrees)
* __Translate__ - translate plane by vector
* __Rotate__ - rotate plane around origin or other point
* __Reflect__ - reflect plane in point, line or plane
* __Equals__ - check if two planes are equals
* __ToString__ - string representation of plane in global or local coordinate system

## Sphere

Defines a sphere in 3D space. Implements intersection with line, plane and other sphere, projection to line and plane, as well as
common translation, rotation and reflection methods.
### Properties
* __Center__ - center of the sphere
* __R__ - radius of the sphere
* __Area__ - area of the sphere
* __Volume__ - volume of the sphere
### Methods
* __Clone__ - deep copy of object
* __DistanceTo__ - shortest distance to point, line, ray, segment or plane
* __IntersectionWith__ - intersection of sphere with line, plane or other sphere
* __ProjectionTo__ - orthogonal projection of sphere to the line or plane
* __Translate__ - translate sphere by vector
* __Rotate__ - rotate sphere around origin or other point
* __Reflect__ - reflect sphere in point, line or plane
* __Equals__ - check if two spheres are equals
* __ToString__ - string representation of sphere in global or local coordinate system

## Circle3d

Defines a circle in 3D space. Implements common translation, rotation and reflection methods.
### Properties
* __Center__ - center of the circle
* __R__ - radius of the circle
* __Normal__ - normal of the circle
* __Perimeter__ - perimeter of the circle
* __Area__ - area of the circle
* __ToEllipse__ - convert circle to equivalent ellipse
### Methods
* __Clone__ - deep copy of object
* __ParametricForm__ - return point on circle for given parameter 't'
* __ProjectionTo__ - orthogonal projection of circle to plane
* __IntersectionWith__ - intersection of circle with plane
* __Translate__ - translate circle by vector
* __Rotate__ - rotate circle around origin or other point
* __Reflect__ - reflect circle in point, line or plane
* __Equals__ - check if two circles are equals
* __ToString__ - string representation of circle in global or local coordinate system

## Ellipse

Defines an ellipse in 3D space, represented by center point and two vectors, for major and minor semiaxes.
### Properties
* __Center__ - center of the ellipse
* __MajorSemiaxis__ - major semiaxis of the ellipse
* __MinorSemiaxis__ - minor semiaxis of the ellipse
* __Normal__ - normal of the ellipse
* __A__ - length of major semiaxis
* __B__ - length of minor semiaxis
* __F__ - distance from center to focus
* __F1__ - first focus
* __F2__ - second focus
* __e__ - eccentricity of the ellipse
* __Perimeter__ - approximate circumference of the ellipse
* __Area__ - area of the ellipse
### Methods
* __Clone__ - deep copy of object
* __ParametricForm__ - return point on ellipse for given parameter 't'
* __ProjectionTo__ - orthogonal projection of ellipse to plane
* __Translate__ - translate ellipse by vector
* __Rotate__ - rotate ellipse around origin or other point
* __Reflect__ - reflect ellipse in point, line or plane
* __Equals__ - check if two ellipses are equals
* __ToString__ - string representation of ellipse in global or local coordinate system

## Triangle

Defines a triangle n 3D space. Implements common translation, rotation and reflection methods. Calculates most of the standard
triangle properties: bisectors, meadians, altitudes, incenter, circumcenter, centroid, orthocenter, etc.
### Properties
* __A/B/C__ - vertices of the triangle
* __AB/AC/BC__ - length of the triangles' sides
* __Perimeter__ - perimeter of the triangle
* __Area__ - area of the triangle
* __Circumcircle__ - circumcircle of the triangle
* __Angle_A/B/C__ - angle at the vertex A/B/C
* __Bisector_A/B/C__ - angle bisector at the vertex A/B/C
* __Incenter__ - incenter of the triangle
* __Centroid__ - centroid of the triangle
* __Orthocenter__ - orthocenter of the triangle
* __Circumcenter__ - circumcenter of the triangle
* __Incircle__ - incircle of the triangle
* __Altitude_A/B/C__ - altitude at the vertex A/B/C
* __Median_A/B/C__ - median at the vertex A/B/C
* __IsEquilateral__ - check if all sides of the triangle are the same length
* __IsIsosceles__ - check if two sides of the triangle are the same length
* __IsScalene__ - check if all sides are unequal
* __IsRight__ - check if one angle is equal 90 degrees
* __IsObtuse__ - check if one angle is greater than 90 degrees
* __IsAcute__ - check if all angles are less than 90 degrees
### Methods
* __Clone__ - deep copy of object
* __Translate__ - translate triangle by vector
* __Rotate__ - rotate triangle around origin or other point
* __Reflect__ - reflect triangle in point, line or plane
* __Equals__ - check if two triangles are equals
* __ToString__ - string representation of triangle in global or local coordinate system

## Coord3d

Class representing orthogonal cartesian 3D coordinate system. Defined by an origin point and transformation matrix
(three orthogonal unit vectors stored in row format). One global coordinate system (Coord3d.GlobalCS) is defined by default,
any number of local coordinate systems can be defined by users.
### Properties
* __Origin__ - origin of the coordinate system
* __Axes__ - unit vectors of the axes, stored as row-matrix(3x3)
* __Name__ - name of the coordinate system
* __Counts__ - total number of defined coordinate systems
* __X/Y/Zaxis__ - X/Y/Z-axis of the coordinate system
* __XY/XZ/YZ_plane__ - planes of the coordinate system
### Methods
* __Clone__ - deep copy of object
* __Rotate/RotateDeg__ - rotate coordinate system around rotation axis
* __Equals__ - check if two coordinate systems are equals
* __ToString__ - string representation of coordinate system

## Matrix3d

### Properties
* __Item(i,j)__ - element of the matrix
* __Row1/2/3__ - rows of the matrix
* __Column1/2/3__ - columns of the matrix
* __Det__ - determinant of the matrix
* __MaxNorm__ - Max norm of the matrix
* __IsZero__ - check if matrix is zero matrix
* __IsIdentity__ - check if matrix is identity matrix
* __IsOrthogonal__ - check if matrix is orthogonal
### Methods
* __Inverse__ - inverse of the matrix
* __Transpose__ - transpose of the matrix
* __RotationMatrix__ - rotation around given axis
* __Equals__ - check if two matrix are equals
* __ToString__ - string representation of matrix

## GeometRi3D

### Properties
* __Tolerance__ - tolerance used for comparison operations (default 1e-12)
### Methods
* __AlmostEqual__ - tolerance based equality check
* __NotEqual__ - tolerance based unequality check
* __Greater__ - tolerance based comparison
* __Smaller__ - tolerance based comparison
