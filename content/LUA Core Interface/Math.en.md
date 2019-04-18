---
title: "Math"
date: 2019-04-13T18:16:49+02:00
draft: false
---

This module contains all the necessary tools to convert and modify typical telemetry data.

Here, we are calling vectors, tables with three components:

	{
		x = number,
		y = number,
		z = number,
	}

#### Math.Angle.Subtract( leftAngle , rightAngle )
*Tacview 1.7.2*

Substracts two radian angles.

{{% notice note %}}
**Return value:**<br>
	Difference between **leftAngle** and **rightAngle**.<br>
	The result is normalized to **[-pi, +pi]**.
{{% /notice %}}


#### Math.Units.FeetToMeters( value )
*Tacview 1.8.0*

Converts feet distances in meters


#### Math.Units.NauticalMilesToMeters( value )
*Tacview 1.8.0*

Converts nautical miles distances in meters


#### Math.Vector.LongitudeLatitudeToCartesian( {longitude = number , latitude = number , altitude = number} )
*Tacview 1.7.2*

Converts Earth spherical coordinates into cartesian coordinates.
It is possible to direcly give an object transform to this function, see [Telemetry.GetCurrentTransform](/telemetry/#telemetry-getcurrenttransform-objecthandle-tacview-1-7-2).

**Longitude** and **latitude** are in radian.
**Altitude** is in meter.

{{% notice note %}}
**Return value:**<br>
	A **vector** which is a the cartesian position in global Earth space.
{{% /notice %}}


#### Math.Vector.CartesianToLongitudeLatitude( {x = number , y = number , z = number} )
*Tacview 1.7.5*

Converts cartesian coordinates into Earth spherical coordinates.

{{% notice note %}}
**Return value:**<br>
	A **table** which contains the { longitude = ... , latitude = ... , altitude = ...}<br>
	Longitude and latitude are in radian.<br>
	Altitude is in meter.
{{% /notice %}}


#### Math.Vector.BearingRangeAltitudeToLongitudeLatitude( referenceLongitude , referenceLatitude , bearing , range , altitude )
*Tacview 1.8.0*

Retrieve longitude, latitude and altitude relative to given reference point.

- Longitude and latitude are expressed in radian.
- Bearing is expressed in degrees relative to true north.
- Range is expressed in meters.
- Altitude is expressed in meters.

{{% notice note %}}
**Return value:**<br>
		Position of the target point as {longitude = number , latitude = number , altitude = number}
{{% /notice %}}


#### Math.Vector.Add( vector1 , vector2 )
*Tacview 1.7.2*

Adds two 3D vectors.

{{% notice note %}}
**Return value:**<br>
	A **vector** wich is the sum of **vector1** and **vector2**.
{{% /notice %}}


#### Math.Vector.Subtract( vector1 , vector2 )
*Tacview 1.7.2*

Substracts two 3D vectors.

{{% notice note %}}
**Return value:**<br>
	A **vector** which is the difference between **vector1** and **vector2**.
{{% /notice %}}


#### Math.Vector.Multiply( factor , vector )
*Tacview 1.7.5*

Multiplies a scalar value by a specified vector.

{{% notice note %}}
**Return value:**<br>
	Scaled **vector**.
{{% /notice %}}


#### Math.Vector.Normalize( vector )
*Tacview 1.7.2*

Normalize the given vector.

{{% notice note %}}
**Return value:**<br>
	Normalized **vector**.<br>
	This function is safe and a nul vector is the vector is nul.
{{% /notice %}}


#### Math.Vector.GetLength( vector ) -- Tacview 1.8.0

Retrieve the length of given vector.


#### Math.Vector.GetDistance( pt1 , pt2 ) -- Tacview 1.8.0

Retrieve the distance between given 3D cartesian points.


#### Math.Vector.GetDistanceOnEarth( longitude1 , latitude1 , longitude2 , latitude2 , altitude ) -- Tacview 1.8.0

Retrieve the distance between the specified coordinates on earth at the given above sea level altitude.


#### Math.Vector.AngleBetween( vector1 , vector2 )
*Tacview 1.7.2*

Calculate the angle between two *normalized* vectors.
{{% notice info %}}
DO NOT forget to normalize the vectors before calling GetAngle!
{{% /notice %}}
{{% notice tip %}}
NOTE: If you want an accurate quadran calculation, you may want to use the function with three parameters.
{{% /notice %}}

{{% notice note %}}
**Return value:**<br>
	**Angle** in radian between the two given vectors.<br>
	Which corresponds to `ArcCos( DotProduct( vector1, vector2 ) )`
{{% /notice %}}


#### Math.Vector.AngleBetween( vector , referenceVector1 , referenceVector2 )
*Tacview 1.7.2*

Calculate the angle between using two normalized vectors.
{{% notice info %}}
DO NOT forget to normalize the vectors before calling GetAngle!
{{% /notice %}}
Unlike **AngleBetween( vector1 , vector2 )**, this function gives the correct quadran.

{{% notice note %}}
**Return value:**<br>
	**Angle** in radian between the two given vectors.<br>
	Which corresponds to `ArcTan( DotProduct( vector, referenceVector1 ), DotProduct( vector, referenceVector2 ) )`
{{% /notice %}}


#### Math.Vector.LocalToGlobal( objectTransform , localCoordinates )
*Tacview 1.7.2*

Converts the given point from an object local coordinates into Earth cartesian coordinates.

You can direcly pass to this function, the **objectTransform** table coming from **Telemetry.GetCurrentTransform()** where **localCoordinates** is a vector.

	objectTransform =
	{
		-- If xyz are not specified, they will be calculated from longitude, latitude, and altitude.

		x = cartesianPositionX,					-- meters
		y = cartesianPositionY,					-- meters
		z = cartesianPositionZ,					-- meters

		-- If either longitude or latitude is not specified, they will be calculated from xyz.

		longitude = sphericalLongitude,			-- radian
		latitude = sphericalLatitude,			-- radian
		altitude = absoluteAltitude,			-- (meters) required only if xyz are not specified

		roll = objectRoll,						-- radian
		pitch = objectPitch,					-- radian
		yaw = objectYaw,						-- radian
	}

{{% notice note %}}
**Return value:**<br>
	**coordinates as a vector** in Earth global cartesian space.<br>
	returns **nil** if not enough data is provided.
{{% /notice %}}
