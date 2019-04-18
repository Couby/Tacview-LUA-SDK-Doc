---
title: "Telemetry"
date: 2019-04-13T18:16:47+02:00
draft: false
---

This module is the heart of Tacview.

Use the telemetry manager to read and write any data for any dynamic object.

#### Telemetry.BeginningOfTime
*Tacview 1.7.5*
#### Telemetry.EndOfTime
*Tacview 1.7.5*

Constants used to specify two special time stamps.

	BeginningOfTime = -3.4028234663853e+38
	EndOfTime = 3.4028234663853e+38

**BeginningOfTime** is typically used to create timeless objects like waypoints or buildings.
**EndOfTime** is usefull for exemple to identify objects still alive at the end of telemetry recording.

If you need the timestamp of telemetry recording start or end, check [Telemetry.GetDataTimeRange()](/Tacview-LUA-SDK-Doc/lua-core-interface/telemetry/#telemetry-getdatatimerange)


#### Telemetry.InvalidPropertyIndex
*Tacview 1.7.5*

Constant used to detect invalid properties.


#### Telemetry.Tags
*Tacview 1.7.3*

Enumeration of bits used to defined object types.

		-- Basic Type

		Telemetry.Tags.FixedWing
		Telemetry.Tags.Rotorcraft

		Telemetry.Tags.Armor
		Telemetry.Tags.AntiAircraft
		Telemetry.Tags.Vehicle
		Telemetry.Tags.Watercraft

		Telemetry.Tags.Human
		Telemetry.Tags.Biologic

		Telemetry.Tags.Missile
		Telemetry.Tags.Rocket
		Telemetry.Tags.Bomb
		Telemetry.Tags.Torpedo
		Telemetry.Tags.Projectile
		Telemetry.Tags.Beam

		Telemetry.Tags.Decoy

		Telemetry.Tags.Building

		Telemetry.Tags.Bullseye
		Telemetry.Tags.Waypoint

Use case exemple to identify an object type as airplane :

	local objectTags = Tacview.Telemetry.GetCurrentTags( objectHandle )

	if (Tacview.Telemetry.AllGivenTagsActive(objectTags, Tacview.Telemetry.Tags.FixedWing)) then
	    this_is_a_plane;
	end


#### Telemetry.Property
*Tacview 1.7.6*

List of the names of the properties natively supported by Tacview.

		-- Text properties

		Telemetry.Property.Text.Callsign
		Telemetry.Property.Text.Event
		Telemetry.Property.Text.Name

		-- Numeric properties

		Telemetry.Property.Numeric.Disabled
		Telemetry.Property.Numeric.EngagementRange


#### Telemetry.Clear()
*Tacview 1.7.2*

Purge all telemetry data currently loaded in memory.

This function does not warn the user, nor it gives him the opportunity to save any data.

This function does not interrupt or stop any recording in progress. It simply purges all the data recorded up to that point.


#### Telemetry.IsEmpty()
*Tacview 1.7.6*

Tells if no at all telemetry is currently loaded in memory.

This include intemporal data.


#### Telemetry.IsLikeEmpty()
*Tacview 1.7.6*

Tells if no significant telemetry is currently loaded in memory.

For example, if no data or only intemporal data is loaded this function returns **true**.

Otherwise it returns **false**.


#### Telemetry.GetDataTimeRange()
*Tacview 1.7.6*

Retrieve the extend of the telemetry data currently loaded in memory.

This excludes any intemporal samples like bullseyes position for example.

{{% notice note %}}
**Return value:**<br>
	{<br>
		beginTime,		-- first sample absolute time<br>
		endTime			-- last sample absolute time<br>
	}
{{% /notice %}}


#### Telemetry.GetCurrentObjectHandle( objectId )
*Tacview 1.7.2*

Retrieves the handle of the specified object at the current update time.

If there are several objects with the same id (for example a player which has spawned in the same aircraft multiple time during the same session), the telemetry manager will return the object which is the most appropriate for the current time frame.

Unlike Ids, objects handles uniquely identify each object currently loaded in memory.

{{% notice note %}}
**Return value:**<br>
		objectHandle (integer)
{{% /notice %}}


#### Telemetry.GetCurrentOrCreateObjectHandle( objectId )
*Tacview 1.7.5*

Retrieves the handle of the specified object at the current update time.

If the give object id is not found, then a new object will be created at the current update time with the given id.

Unlike Ids, objects handles uniquely identify each object currently loaded in memory.

{{% notice note %}}
**Return value:**<br>
		objectHandle (integer)
{{% /notice %}}


#### Telemetry.GetOrCreateObjectHandle( objectId , absoluteTime )
*Tacview 1.7.5*

Retrieves the handle of the specified object at the specified time.

If the given object id is not found, then a new object will be created at the specified time with the given id.

Unlike Ids, objects handles uniquely identify each object currently loaded in memory.

To create a timeless object like a waypoint, you can use the following:
`local newObjectHandle = Tacview.Telemetry.GetOrCreateObjectHandle( objectId , Tacview.Telemetry.BeginningOfTime )`

{{% notice note %}}
**Return value:**<br>
		objectHandle (integer)
{{% /notice %}}


#### Telemetry.GetCurrentTags( objectHandle )
*Tacview 1.7.3*

Return given object tags as a bit field.

{{% notice note %}}
**Return value:**<br>
		Each bit of the returned integer corresponds to a specific tag.<br>
		The combination of these tags defines the current object type.<br>
		The object type can evolve over time and be refined depending on available telemetry at this point.
{{% /notice %}}


#### Telemetry.GetCurrentShortName( objectHandle )
*Tacview 1.7.2*

Return given object short name at the current update time.

{{% notice note %}}
**Return value:**<br>
		Text which typically correspond to the NATO code or any other appropriate short designation for the object.
{{% /notice %}}


#### Telemetry.GetTransform( objectHandle , absoluteTime )
*Tacview 1.7.5*
#### Telemetry.GetCurrentTransform( objectHandle )
*Tacview 1.7.2*

Returns given object position/rotation at the current update or specified time.

Some objects (typically bullets) may not have all the information available.

For example, the rotation information may not be available for all aircraft.

Native coordinates correspond the original coordinates in the source flight simulator (typically for BMS and DCS).

{{% notice note %}}
**Return value:**<br>
{{% /notice %}}

		ObjectTransform =
		{
			time = sample_absolute_time,			-- (seconds) This effective absolute time of this sample may be different from current update time if the object does not exist yet, or anymore...

			x = cartesianPositionX,					-- (meters) Cartesian position (ALWAYS AVAILABLE)
			y = cartesianPositionY,					-- (meters) Cartesian position (ALWAYS AVAILABLE)
			z = cartesianPositionZ,					-- (meters) Cartesian position (ALWAYS AVAILABLE)

			longitude = sphericalLongitude,			-- (radian) Spherical position (ALWAYS AVAILABLE)
			latitude = sphericalLatitude,			-- (radian) Spherical position (ALWAYS AVAILABLE)
			altitude = absoluteAltitude,			-- (meters) Spherical position (ALWAYS AVAILABLE)

			roll = objectRoll,						-- (radian) roll  axis rotation (if rotationIsValid == true)
			pitch = objectPitch,					-- (radian) pitch axis rotation (if rotationIsValid == true)
			yaw = objectYaw,						-- (radian) yaw   axis rotation (if rotationIsValid == true)

			u = nativePositionX,					-- (meters) Native x coordinate (if nativeCoordinatesAreValid == true)
			v = nativePositionY,					-- (meters) Native y coordinate (if nativeCoordinatesAreValid == true)
			heading = nativeHeadingToNorth,			-- (radian) Heading in native coordinates system (if nativeCoordinatesAreValid == true & rotationIsValid == true)

			rotationIsValid = boolean,				-- Set to true if rotation information is valid (otherwise the data may be emulated)
			nativeCoordinatesAreValid = boolean,	-- Set to true if native coordinates are valid (otherwise u, v and heading are set to zero)
		}

{{% notice note %}}
**Return value:**<br>
		value , validity<br>
		validity is set to false if the value does not really apply for the given time (typically if the object does not exist at the given time) event when validity is set to false, the value is valid and usable (this simplify the client code)
{{% /notice %}}


#### Telemetry.GetCurrentVerticalGForce( objectHandle )
*Tacview 1.7.3*

Returns given object vertical G-Force if available at current time.

If vertical G-Force has been recorded, then Tacview will return the interpolated sample.

If vertical G-Force has not been recorded, but rotation data is available, Tacview will calculate the vertical G-Force.

{{% notice note %}}
**Return value:**<br>
		**Vertical G-Force** if available.<br>
		**nil** when not enough data is available (or object does not exist at this time).
{{% /notice %}}


#### Telemetry.GetGlobalNumericPropertyIndex( propertyName , autoCreate )
*Tacview 1.7.6*
#### Telemetry.GetGlobalTextPropertyIndex( propertyName , autoCreate )
*Tacview 1.7.6*

Retrieve a property for the global object (0).

If the property does not exist yet:

- if autoCreate is true, then the property will be created and its index returned.
- if autoCreate is false, then Telemetry.InvalidPropertyIndex will be returned.

To optimize CPU and memory, numeric and text properties are separate in the telemetry manager.

{{% notice info %}}
**WARNING:** Because numeric and text properties are separate, indexes for numeric and text samples may overlap and cannot be mixed.
{{% /notice %}}


#### Telemetry.GetObjectsNumericPropertyIndex( propertyName , autoCreate )
*Tacview 1.7.5*
#### Telemetry.GetObjectsTextPropertyIndex( propertyName , autoCreate )
*Tacview 1.7.5*

Retrieve a property index for everything which is not the global object.

The index returned is the same for all objects.

If the property does not exist yet:

- if autoCreate is true, then the property will be created and its index returned.
- if autoCreate is false, then Telemetry.InvalidPropertyIndex will be returned.

To optimize CPU and memory, numeric and text properties are separate in the telemetry manager.

{{% notice info %}}
**WARNING:** Because numeric and text properties are separate, indexes for numeric and text samples may overlap and cannot be mixed.
{{% /notice %}}


#### Telemetry.GetNumericSample( objectHandle , absoluteTime , propertyIndex )
*Tacview 1.7.5*
#### Telemetry.GetTextSample( objectHandle , absoluteTime , propertyIndex )
*Tacview 1.7.5*

Retrieve property numeric or text value at the given time.

{{% notice note %}}
**Return value:**<br>
		value , validity<br>
		validity is set to false if the value does not really apply for the given time (typically if the object does not exist at the given time) event when validity is set to false, the value is valid and usable (this simplify the client code)
{{% /notice %}}


#### Telemetry.SetNumericSample( objectHandle , absoluteTime , propertyIndex , value )
*Tacview 1.7.5*
#### Telemetry.SetTextSample( objectHandle , absoluteTime , propertyIndex , value )
*Tacview 1.7.5*

Set or re-set given numeric or text property value at the given time.

You can set **absoluteTime** to **Tacview.Telemetry.BeginningOfTime** to declare the properties of timeless objects like waypoints.


#### Telemetry.SetTransform( objectHandle , absoluteTime , transform )
*Tacview 1.7.5*

Set or re-set object position and rotation at the given time.

**absoluteTime** is a 64-bit floating point number which represents the number of seconds elapsed to 1970-01-01T00:00:00Z

Injected angles (including longitude and latitude) MUST be normalized between ]-pi,+pi]

Failure to do so may produce undefined results with some formulas.

For performance reasons, angles retrieved by the telemetry manager are **NOT** always normalized between ]-pi,+pi]

Do not forget to normalize angles before displaying then as text to the final user!

-- non specified members will be set to the interpolated value of the preceding and following samples.

	transform
	{
		-- Spherical position

		f64 longitude;		-- (radian) Spherical position (+ is towards east)
		f64 latitude;		-- (radian) Spherical position (+ is towards north)
		f32 altitude;		-- (meters) Spherical position

		-- Rotation

		f32 roll;			-- (radian) roll axis rotation
		f32 pitch;			-- (radian) pitch axis rotation
		f32 yaw;			-- (radian) yaw axis rotation

		-- Native coordinates, mostly used to get accurate distance and speed calculation for flat world simulators.

		f32 u;				-- (meters) Native x coordinate
		f32 v;				-- (meters) Native y coordinate
		f32 heading;		-- (radian) Heading in native coordinates system
	};


#### Telemetry.GetLifeTime( objectHandle )
*Tacview 1.7.6*

Return absolute time of the object first appearance and its time of disappearance if applicable.

{{% notice note %}}
**Return value:**<br>
		lifeTimeBegin, lifeTimeEnd
{{% /notice %}}

If the object exists from the beginning of times (e.g. a bullseye) its **lifeTimeBegin** is **Telemetry.BeginningOfTime**.

If the object has never been destroyed or removed from the battlefield, then **lifeTimeEnd** is **Telemetry.EndOfTime**.


#### Telemetry.SetLifeTimeEnd( objectHandle , absoluteTime )
*Tacview 1.7.5*

Defines the end-of-life of the specified object.

Typically used to specify when an object has been destroyed or has been removed from the battlefield.


#### Telemetry.DeleteObject( objectHandle )
*Tacview 1.7.5*

Remove the specified object from the telemetry manager.

This operation is safe: The corresponding handle will remain valid until the next effective purge (typically when loading a new telemetry file) so the other modules will not crash if they attempt to reference the object afterward.

However, any data related to this object will be freed.


#### Telemetry.GetObjectCount()
*Tacview 1.7.6*

Retrieve the total number of objects currently active in the telemetry manager.

Typically used to enumerate all objects.


#### Telemetry.GetObjectHandleByIndex( index )
*Tacview 1.7.6*

Retrieve an object by its index.
{{% notice tip %}}
**NOTE:** The index goes from **0** to **GetObjectCount() - 1**.
{{% /notice %}}

{{% notice note %}}
**Return value:**<br>
		The object **handle** or **nil** if the index is out of range.
{{% /notice %}}


#### Telemetry.GetObjectId( objectHandle )
*Tacview 1.7.6*

Retrieve given object id.

Beware that object ids can be recycled and cannot uniquely identify objects.

For that reason, avoid using them, unless it is for telemetry injection (event creation) or export.
