# IOOS Convention for Observing Asset Identifiers (Next Draft)

Authors: Jeff de La Beaujardière, NOAA/NESDIS/Technology Planning and Integration Office
Contributors: Derrick Snowden, Carmel Ortiz, and Alex Birger, U.S. IOOS Office;
Anna Milan, Metadata Specialist at NOAA National Geophysical Data Center (NGDC).

## Introduction

This document describes the convention used by the Integrated Ocean Observing System (IOOS) program
to assign an identifier to IOOS-related observing assets including measurement stations, platforms
and sensors. An identifier is used as the name by which further metadata about the asset may be
requested from IOOS web services. An IOOS identifier is the name that IOOS web services uses for the
asset, but each asset may also have other names assigned by other communities.

Many assets have numbers or labels assigned to them by an external authority. For example, every weather
buoy has a World Meteorological Organization (WMO) number. The IOOS identifiers allow for and make use of
such identifiers. However, rather than merely using the number (e.g., 42001) which could refer to a buoy
in the Gulf of Mexico or the postal code for Paducah, Kentucky or the section of the California Vehicle Code
that describes fines imposed for moving violations, the IOOS identifiers add some semantics to indicate
(a) the authority which assigned the number or name and (b) that the asset is somehow associated with IOOS.
Being "associated with IOOS" in this context typically means that data from that asset could be discovered
or accessed through the IOOS data management layer \[Needs reference\].

## Revision History

| Version | Description              | Date       |
|---------|--------------------------|------------|
| 0.0.1   | First draft.             | 2010-12-22 |
| 0.1     | Updated draft            | 2013-12-06 |
| 0.5     | Updated for Milestone 1.0| 2014-08-31 |

## Informative Examples

For the sake of illustration, we first provide examples of identifiers in use by IOOS. Later sections of this
document constitute the actual specification of those identifiers.  In the case of conflict or ambiguity, the
specification sections take precedence over these examples.

| Asset      |  Identifier   |
|--------    | ------------  |
| WMO buoy 42001 | __`urn:ioos:station:wmo:42001`__ |
|Wave sensor on WMO buoy 42001|__`urn:ioos:station:wmo:42001:wpm1`__ |
|CO-OPS station cb0102 |__`urn:ioos:station:NOAA.NOS.CO-OPS:cb0102`__ |
|Active water level sensors within CO-OPS network of stations | __`urn:ioos:network:NOAA.NOS.CO-OPS:WaterLevelActive`__ |
|Water level sensor at CO-OPS station 8454000 | __`urn:ioos:sensor:NOAA.NOS.CO-OPS:8454000:D1`__ |
|Nortek Acoustic Doppler Profiler sensor that is measuring water currents and/or waves and is mounted on the CO-OPS cb0201 station | __`urn:ioos:sensor:NOAA.NOS.CO-OPS:cb0201:Nortek-ADP-514`__ |

# General Identifier Convention

## Use of Uniform Resource Names

An IOOS identifier is a Uniform Resource Name (URN). URNs are commonly used as identifiers in the Internet’s
information architecture. An introductory description of URNs may be found on
[Wikipedia](http://en.wikipedia.org/wiki/Uniform_Resource_Name). Some of the material in this section is
based on definitions and restrictions established by Internet
[Engineering Task Force (IETF) Request for Comments (RFC) 2141](http://tools.ietf.org/html/rfc2141).

All URNs assigned by IOOS begin with the string __`urn:ioos:`__, followed by one or more fields also separated
by colons (__`:`__). The initial __`urn:`__ indicates that the identifier is a URN. The following __`ioos:`__
indicates that the URN is in the IOOS namespace.

_**NOTE**: IOOS intended to formally register the **ioos** namespace with IANA, but has not done it
yet (2010-12-22) has not._

The additional fields may only include letters and numbers (_**A-Z**_, _**a-z**_, _**0-9**_) and the
following characters: _**( ) + , - . = @ ; $ _ ! \***_

Special characters not in the foregoing list must be represented using hexadecimal encoding as _**%xx**_,
where **xx** represents a two-digit hex value. The use of such characters in IOOS URNs is not recommended.

## Case-insensitivity

IOOS URNs are considered to be case-insensitive. Example: `urn:ioos:ABC` and `urn:ioos:abc` refer to the same thing.
This is more restrictive than, but permitted by, IETF RFC 2141.  The fields in IOOS URNs are customarily lower-case
but may appear in uppercase or mixed-case.

## Identifier Pattern

The general pattern for IOOS asset identifiers is

__`urn:ioos:asset_type:authority:label[:component]`__

which consists of the following fields delimited by __`:`__.

>__`urn:ioos`__ a fixed string indicating this is an IOOS URN;

>__`asset_type`__ a variable indicating the type of asset being identified;

>__`authority`__ an abbreviation or name for the organization that assigned the label;

>__`label`__ the number or label that was assigned by the authority to the asset;

>__`component`__ an optional field naming a specific component.

The following sections explain in details the use of all variable fields.  Ideally these fields will be
populated with values from community governed controlled vocabularies.  While this is not mandated by this
specification, some candidate vocabularies are suggested in the following sections.

### Asset Type

The __`asset_type`__ field indicates the type of asset to which this identifier applies. The following values
for __`asset_type`__ are recognized by IOOS:

#### station

>A fixed installation or nominally-constant position where measurements are performed.  Examples include: a
water-level gauge mounted on a pier; a moored buoy that moves within a known watch radius of the nominal
mooring location; an OceanSITES deep-water monitoring location; a site at which water quality samples are taken.
A __`component`__ field may be added to the URN to identify a specific sensor located at the station.
If __`component`__ field is omitted, the URN identifies station itself.

#### network

>A network of stations defined above. 

#### sensor

>A device associated with the station that measures one or more observed quantities at or adjacent to the
station location. Examples include: a water-level sensor; a temperature sensor; an anemometer; a current meter.
A sensor identifier URN includes the __`authority`__ and __`label`__ fields of the station, and a __`component`__
field to distinguish it from other sensors at the same station. Note that __`label`__ for sensor is different
from __`label`__ for station.

#### survey

>A visual observation, measurement or collecting samples by a human observer performed at a station or from a ship
for a follow-up analyzes in the laboratory. Example: a quarterly visit to a known location to collect water
for chemical analysis; an assessment by a diver of the species present in a particular location, etc.

Additional __`asset_type`__ values may be added by IOOS as needed.  Candidate controlled vocabularies that may
be adopted as the valid values in the __`asset_type`__ field are:

* [Marine Metadata Initiative Device Ontology](http://mmisw.org/orr/#http://mmisw.org/ont/mmi/device)
* [BODC Instruments List](http://mmisw.org/orr/#http://vocab.ndg.nerc.ac.uk/list/L221/current)
* [GCMD Instrument types](http://gcmdservices.gsfc.nasa.gov/static/kms/instruments/instruments.csv)

### Authority

The __`authority`__ field indicates the organization that assigned the label for this asset. There is no fixed
set of values, because additional authorities may become relevant as new observing systems are connected to IOOS.
However, the same abbreviation or name should be used for all instances of a particular authority. These
abbreviations are case insensitive.  The following values for __`authority`__ are currently used in IOOS:

#### wmo

>World Meteorological Association.

#### noaa.nos.co-ops

>Center for Operational Oceanographic Products and Services (COOPS) in the National Ocean Service (NOS) of the
U.S. National Oceanic and Atmospheric Administration (NOAA).

#### usace

>U.S. Army Corps of Engineers.

#### fiu

>Florida International University.

#### test

>Temporary service instance using for test.

Candidate controlled vocabularies that may be adopted as valid values for the __`authority`__ field include:

* GCMD Keywords
  * Data Centers: http://gcmdservices.gsfc.nasa.gov/static/kms/providers/providers.csv
  * Projects: http://gcmdservices.gsfc.nasa.gov/static/kms/projects/projects.csv

### Label

The __`label`__ is a number or string assigned by the Authority to the asset. Allowed values are defined by the
particular authority. The only restrictions are that (a) the characters used must not conflict with the URN
specification (see section 2.1) and (b) labels in the scope of a given authority must be unique.
The __`label`__ value varies between station and sensor URNs.

### Component

The __`component`__ field is used to distinguish between different assets associated with the same parent asset.
For example, a buoy may have multiple sensors attached to it, and each sensor will have an identifier that includes
the label for the buoy and the label for the sensor.  The component label must be unique for each
__`asset_type:authority:label`__.


# Convention for Specific Asset Types

## Station Identifiers

The pattern for IOOS platform identifiers is __`urn:ioos:station:authority:label[:version]`__.
Platform identifiers do not include a __`component`__ field.

## Sensor Identifiers

The pattern for IOOS sensor identifiers may be either

__`urn:ioos:sensor:authority:label_sensor[:version]`__

or

__`urn:ioos:station:authority:label_station:component[:version]`__


Depending on the option, sensor is identified either by its __`label_sensor`__, or by a station __`component`___ field,
which provides a name for the sensor.  The specific names are at the discretion of the organization operating the sensor
or the service to access data from the sensor. The __`component`__ and __`label_sensor`__ values may vary for the same
sensor, and may reflect the make and model of the sensor (e.g., `SONTEK-ADP-419`), the phenomenon observed by that
sensor (e.g., `salinity`), or an arbitrary label used by the organization (e.g., `A1`). The name may not include
characters not allowed in Section 3.1.

### Version

Currently, IOOS Convention does not regulate asset versioning; therefore, no requirements have been established for
the version number report. It is strongly recommended to avoid referring to any version number at all in asset's URN.

## Survey Identifiers

A survey identifier URN includes the __`authority`__ and __`label`__ fields of the station or a ship, and a __`component`__
field to distinguish it from other surveys at the same station or ship:

__`urn:ioos:survey:authority:label[:component]`__

For visual observation purpose, the __`authority`__,  __`label`__, and __`component`__ fields may also indicate either
(1) the general observing protocol or (2) the specific type of observation.

### General observing protocol

If visual estimates are made according to some established observing protocol, then the __`authority`__ field may contain
a reference to the document that describes the protocol. For example, if observation was made by the
[NWS Observing Handbook No. 1 (2004)](http://www.vos.noaa.gov/ObsHB-508/ObservingHandbook1_2004_508_compliant.pdf),
then the survey identifier will look as follows:

__`urn:ioos:survey:nws_observing_handbook_2004:label[:component]`__

If a simple reference to the document is sufficient to avoid any need for additional interpretation, it is acceptable to
identify the survey with just the URL of the document describing the observing protocol, laboratory procedures, etc.
In the case of the NWS Observing Handbook, for example, the following URL may play a role of the survey ID:

_**http://www.vos.noaa.gov/ObsHB-508/ObservingHandbook1_2004_508_compliant.pdf**_

### Specific type of observation

The survey identifier may include the type of observation made by the human. For example, in the NWS Handbook, Chapter 2,
page 2-7 says that "iw" is the "wind speed indicator", and that it has values 0, 1, 3, 4 depending on how the wind speed
was estimated or measured, with "3" being "wind speed estimated in knots." For such an observation, the survey identifier
may use the observation code instead of __`authority`__,  __`label`__, and __`component`__ fields:

__`urn:ioos:survey:iw:3`__

or in a more verbose manner:

__`urn:ioos:survey:wind_speed_indicator:estimated_in_knots`__

Similarly, from p.2-76, sea surface temperature measurement can be identified as  

__`urn:ioos:survey:ss:1`__

or
 
__`urn:ioos:survey:sst_indicator:negative_intake_measurement`__
