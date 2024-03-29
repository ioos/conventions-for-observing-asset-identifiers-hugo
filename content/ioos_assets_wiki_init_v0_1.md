+++
draft = false
title = "IOOS Convention for Asset Identification v0.1"
description = "INITIAL VERSION"
type = "post"
date = 2014-08-04T08:10:23Z
sidebar = true
weight = "90"
+++


_Initial version of the guidance for the asset identification process. For the data to be discoverable and accessible through the IOOS Data Catalog, all observing assets must be identified in accord with the present IOOS Convention.<br><b>DEPRECATED. </b>_
<!--more-->
<br><br>



# Revision History 

| Version | Description | Date |
|---------|-------------|----- |
| 0.0.1 | First draft | 2010-12-22 |
| 0.1 | Streamlined and cleaned up draft | 2013-12-06 |


<p style="color:red; font-size:120%; border:3px solid red; padding:15px;"> DISCLAIMER: This is an <b>OBSOLETE</b> initial version of the document that was <b>DEPRECATED</b> as an official IOOS document. <br>Please <b>DO NOT</b> refer to this publication.</p>
<p>
<br>

# Contributors

| Name  | Role | Association  |
|:---|:---|:----|
|Jeff de La Beaujardière | Author| NOAA/NESDIS/Technology Planning and Integration Office |
|Derrick Snowden | Contributor | U.S. IOOS Office |
|Carmel Ortiz | Contributor | U.S. IOOS Office | 
|Alex Birger | Contributor | U.S. IOOS Office |
|Anna Milan | Contributor | NOAA National Geophysical Data Center (NGDC) |


# References

[**IETF RFC 2141**](http://tools.ietf.org/html/rfc2141-http://tools.ietf.org/html/rfc2141)

<br>
<br>

# Informative Examples #

For the sake of illustration, we first provide examples of identifiers in use by IOOS. Later sections of this document constitute the actual specification of those identifiers.  In the case of conflict or ambiguity, the specification sections take precedence over these examples. 
<br>


| Asset      |  Identifier   |
|--------    | ------------  |
| WMO buoy 42001 | urn:ioos:station:wmo:42001 |
|Wave sensor on WMO buoy 42001|urn:ioos:station:wmo:42001:wpm1 |
|CO-OPS station cb0102 |urn:ioos:station:NOAA.NOS.CO-OPS:cb0102 |
|Active water level sensors within CO-OPS network of stations | urn:ioos:network:NOAA.NOS.CO-OPS:WaterLevelActive |
|Water level sensor at CO-OPS station 8454000 | urn:ioos:sensor:NOAA.NOS.CO-OPS:8454000:D1 |
|Nortek Acoustic Doppler Profiler sensor that is measuring water currents and/or waves and is mounted on the CO-OPS cb0201 station | style=white-space:nowrap |  urn:ioos:sensor:NOAA.NOS.CO-OPS:cb0201:Nortek-ADP-514 |
<br>

# General Identifier Convention

## Use of Uniform Resource Names

An IOOS identifier is a Uniform Resource Name (URN). URNs are commonly used as identifiers in the Internet\’s information architecture. An introductory description of URNs may be found on [Wikipedia](http://en.wikipedia.org/wiki/Uniform_Resource_Name). Some of the material in this section is based on definitions and restrictions established by Internet [Engineering Task Force (IETF) Request for Comments (RFC) 2141](http://tools.ietf.org/html/rfc2141).

All URNs assigned by IOOS begin with the string _**urn:ioos:**_, followed by one or more fields also separated by colons (_**:**_). The initial _**urn:**_ indicates that the identifier is a URN. The following _**ioos:**_ indicates that the URN is in the IOOS namespace.

_**NOTE**: IOOS intended to formally register the **ioos** namespace with IANA, but has not done it yet (2010-12-22) has not._

The additional fields may only include letters and numbers (_**A-Z**_, _**a-z**_, _**0-9**_) and the following characters: _**( ) + , - . = @ ; $ _ ! \***_

Special characters not in the foregoing list must be represented using hexadecimal encoding as _**%xx**_, where **xx** represents a two-digit hex value. The use of such characters in IOOS URNs is not recommended.
<br>

## Case-insensitivity

IOOS URNs are considered to be case-insensitive. Example: _**urn:ioos:ABC**_ and _**urn:ioos:abc**_ refer to the same thing. This is more restrictive than, but permitted by, IETF RFC 2141.  The fields in IOOS URNs are customarily lower-case but may appear in uppercase or mixed-case.
<br>

## Identifier Pattern

The general pattern for IOOS asset identifiers is

`urn:ioos:asset_type:authority:label[:component]`

which consists of the following fields delimited by "_**:**_":

_**urn:ioos**_

>a fixed string indicating this is an IOOS URN;

_**asset_type**_

>a variable indicating the type of asset being identified;

_**authority**_

>an abbreviation or name for the organization that assigned the label;

_**label**_

>the number or label that was assigned by the authority to the asset;

_**component**_

>an optional field naming a specific component.

The following sections explain in details the use of all variable fields.  Ideally these fields will be populated with values from community governed controlled vocabularies.  While this is not mandated by this specification, some candidate vocabularies are suggested in the following sections.
<br>

### Asset Type

The _**asset_type**_ field indicates the type of asset to which this identifier applies. The following values for _**asset_type**_ are recognized by IOOS:

**station**

>A fixed installation or nominally-constant position where measurements are performed.  Examples include: a water-level gauge mounted on a pier; a moored buoy that moves within a known watch radius of the nominal mooring location; an OceanSITES deep-water monitoring location; a site at which water quality samples are taken. 
>
>A _**component**_ field may be added to the URN to identify a specific sensor located at the station. If _**component**_ field is omitted, the URN identifies station itself. 

**network**

>A network of stations defined above. 

**sensor**

>A device associated with the station that measures one or more observed quantities at or adjacent to the station location. Examples include: a water-level sensor; a temperature sensor; an anemometer; a current meter. A sensor identifier URN includes the _**authority**_ and _**label**_ fields of the station, and a _**component**_ field to distinguish it from other sensors at the same station. Note that _**label**_ for sensor is different from _**label**_ for station.

**survey**

>A visual observation, measurement or collecting samples by a human observer performed at a station or from a ship for a follow-up analyzes in the laboratory.
>Example: a quarterly visit to a known location to collect water for chemical analysis; an assessment by a diver of the species present in a particular location, etc.

Additional _**asset_type**_ values may be added by IOOS as needed.  Candidate controlled vocabularies that may be adopted as the valid values in the _**asset_type**_ field are:
* [Marine Metadata Initiative Device Ontology](http://mmisw.org/orr/#http://mmisw.org/ont/mmi/device)
* [BODC Instruments List](http://mmisw.org/orr/#http://vocab.ndg.nerc.ac.uk/list/L221/current)
* [GCMD Instrument types](http://gcmdservices.gsfc.nasa.gov/static/kms/instruments/instruments.csv)
<br>

### Authority

The _**authority**_ field indicates the organization that assigned the label for this asset. There is no fixed set of values, because additional authorities may become relevant as new observing systems are connected to IOOS. However, the same abbreviation or name should be used for all instances of a particular authority. These abbreviations are case insensitive.  The following values for _**authority**_ are currently used in IOOS:

**wmo**

>World Meteorological Association.

**noaa.nos.co-ops**

>Center for Operational Oceanographic Products and Services (COOPS) in the National Ocean Service (NOS) of the U.S. National Oceanic and Atmospheric Administration (NOAA).

**usace**

>U.S. Army Corps of Engineers.

**fiu**

>Florida International University.

**test**

>Temporary service instance using for test.

Candidate controlled vocabularies that may be adopted as valid values for the _**authority**_ field include:

* GCMD Keywords
  * Data Centers: http://gcmdservices.gsfc.nasa.gov/static/kms/providers/providers.csv
  * Projects: http://gcmdservices.gsfc.nasa.gov/static/kms/projects/projects.csv
<br>

### Label

The _**label**_ is a number or string assigned by the Authority to the asset. Allowed values are defined by the particular authority. The only restrictions are that (a) the characters used must not conflict with the URN specification (see section 2.1) and (b) labels in the scope of a given authority must be unique.
The _**label**_ value varies between station and sensor URNs.
<br>

### Component

The _**component**_ field is used to distinguish between different assets associated with the same parent asset. For example, a buoy may have multiple sensors attached to it, and each sensor will have an identifier that includes the label for the buoy and the label for the sensor.  The component label must be unique for each _**asset\_type**_:_**authority**_:_**label**_.
<br>



# Convention for Specific Asset Types

## Station Identifiers

The pattern for IOOS platform identifiers is _**urn:ioos:station:authority:label\[:version\]**_
Platform identifiers do not include a _**component**_ field.
<br>

## Sensor Identifiers ##

The pattern for IOOS sensor identifiers may be either

_**urn:ioos:sensor:authority:label_sensor[:version]**_

or

_**urn:ioos:station:authority:label_station:component[:version]**_


Depending on the option, sensor is identified either by its _**label_sensor**_, or by a station _**component**_ field, which provides a name for the sensor.  The specific names are at the discretion of the organization operating the sensor or the service to access data from the sensor. The _**component**_ and _**label_sensor**_ values may vary for the same sensor, and may reflect the make and model of the sensor (e.g., ''SONTEK-ADP-419''), the phenomenon observed by that sensor (e.g., ''salinity''), or an arbitrary label used by the organization (e.g., ''A1''). The name may not include characters not allowed in Section 3.1.
<br>

### Version ###

Currently, IOOS Convention does not regulate asset versioning; therefore, no requirements have been established for the version number report. It is strongly recommended to avoid referring to any version number at all in asset's URN.
<br>

## Survey Identifiers ##

(To be discussed)

## Visual Observations from Ships ##

(this is probably the same as survey identifiers)

Observer (i.e. _**urn:ioos:observer:...**_) seems just as good as other choices. 

I think it would be good to also indicate either (1) the general observing protocol or (2) the specific type of observation, as follows: 

### General observing protocol ###

If visual estimates are made according to, for example, the [NWS Observing Handbook No. 1 (2004)](http://www.vos.noaa.gov/ObsHB-508/ObservingHandbook1_2004_508_compliant.pdf), then perhaps the so-called “sensor” ID could be something like 

_**<urn:ioos:observer:nws_observing_handbook:2004>**_

Indeed, instead of inventing our own URI for this case perhaps we should just insert the URL of the observing protocol: 

http://www.vos.noaa.gov/ObsHB-508/ObservingHandbook1_2004_508_compliant.pdf

This avoids any need for additional interpretation. In the IOOS water quality project we have seen another case where the “metadata” about the measurement procedure is a PDF file containing descriptions of laboratory procedures. 

### Specific type of observation ###

The identifier could include the type of observation made by the human. 

For example, in the Handbook, Chapter 2, page 2-7 says "iw" is the “wind speed indicator” and that it has values 0,1,3,4 depending on how the wind speed was estimated or measured, with "3" being “wind speed estimated in knots.” We could, for example, use 

_**<urn:ioos:observer:iw:3>**_

as the “sensor” ID for such an observation.  Or, we could be less cryptic (since we are not so bandwidth-constrained these days) and expand that out: 

_**<urn:ioos:observer:wind_speed_indicator:estimated_in_knots>**_

Similarly, from p.2-76, sea surface temperature measurement could use 

_**<urn:ioos:observer:ss:1>**_
_**<urn:ioos:observer:sst_indicator:negative_intake_measurement>**_

Personally, I think the cryptic VOS codes could be recorded as-is in the DB because that is presumably what you’re getting on input, and then on output they could be converted to something more readable. 

I don’t know whether (1) or (2) or neither is best. I’m assuming that some data users need to know information like iw=3 and ss=1.



 


