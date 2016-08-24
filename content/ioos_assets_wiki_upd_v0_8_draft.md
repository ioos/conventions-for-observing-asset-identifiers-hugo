+++
draft = false
title = "IOOS Convention for Asset Identification (next draft)"
description = "bla-bla-bla"
type = "post"
date = 2016-07-04T08:10:23Z
sidebar = true
weight = "30"
+++


_This <b>DRAFT</b> document is a proposed update to the current IOOS Convention for Asset Identification; it is published for discussion within IOOS community about the enhanced identification of <b>gliders</b>, and <b>sensors</b>._
<!--more-->
<br><br>

# Revision History


| Version | Description | Date  |
|:--- |:--- |:--- |
| 0.0.1 | First draft | 2010-12-22 |
| 0.1 | Updated draft | 2013-12-06 |
| 0.5 | Updated for Milestone 1.0| 2014-08-31 |
| 0.8 | Updated to enhance sensor identification| 2016-07-15 |


# Contributors

| Name  | Role | Association  |
|:---|:---|:----|
|Jeff de La Beaujardière | Author| NOAA/NESDIS/Technology Planning and Integration Office |
|Derrick Snowden | Contributor | U.S. IOOS Office |
|Carmel Ortiz | Contributor | U.S. IOOS Office | 
|Alex Birger | Contributor | U.S. IOOS Office |
|Anna Milan | Contributor | NOAA National Geophysical Data Center (NGDC) |

<br>
<br>

<p style="color:red; font-size:150%; border:3px solid red; padding:15px;"> <b>DISCLAIMER:</b> This publication is a <b>Discussion Paper</b>, and by no means it should be referred to as an official IOOS document. </p>
<p>
<br>

# Introduction

This document describes the convention used by the Integrated Ocean Observing System (IOOS) program to assign an identifier to IOOS-related observing assets. The observing asset may include hardware units (like measurement platforms and sensors), processes (such as surveys) or their combination. An identifier is used as the name by which further metadata about the asset may be requested from IOOS web services. An IOOS identifier is the name that IOOS web services uses for the asset, but each asset may also have other names assigned by other communities.

Many assets have codes or labels assigned to them by an external authority. For example, every weather buoy has a [World Meteorological Organization (WMO) number](http://www.wmo.int/pages/prog/amp/mmop/wmo-number-rules.html); every registered vessel has an [International Maritime Organization (IMO) number](http://www.imonumbers.lrfairplay.com) assigned by Lloyd's register. The IOOS identifiers allow for and make use of such codes; however, the IOOS identifiers add some semantics to indicate

  * the authority which assigned the number or name;
  * the asset's association with IOOS;
  * the asset application's specifics for measuring of an observed phenomenon.
 
The _**"association with IOOS"**_ in this context typically means that the asset gets exposed through one or more of web services implemented by regional and federal data providers and registered in the IOOS Service Registry, and the asset is the source of a data that can be discovered through the IOOS Catalog.

The _**"asset application's specifics"**_ generally means that along with a hardware component, the asset identifier encompasses some associated processing method or procedure. The inclusion of the basic procedure description into the asset identifier allows to facilitate the data discovery for some specific use cases such as repeated deployment of the same asset, or use of multiple identical assets for observing the identical phenomenon with various reference datums and/or post-processing applied. 

# Informative Examples

For the sake of illustration, the following examples of identifiers are currently in use by IOOS. In the case of conflict or ambiguity, the specification sections take precedence over these examples.

| Asset      |  Identifier   |
|--------    | ------------  |
|WMO buoy 41012|**`urn:ioos:station:wmo:41012`** |
|Wave sensor on WMO buoy 41012|**`urn:ioos:sensor:wmo:41012:wpm1`** |
|CO-OPS station cb0102 |**`urn:ioos:station:NOAA.NOS.CO-OPS:cb0102`** |
|Active water level sensors within CO-OPS network of stations | **`urn:ioos:network:NOAA.NOS.CO-OPS:WaterLevelActive`** |
|Water level sensor at CO-OPS station 8454000 | **`urn:ioos:sensor:NOAA.NOS.CO-OPS:8454000:D1`** |
|Nortek Acoustic Doppler Profiler sensor that is measuring water currents and/or waves and is mounted on the CO-OPS cb0201 station | **`urn:ioos:sensor:NOAA.NOS.CO-OPS:cb0201:Nortek-ADP-514`** |

# General Identifier Convention

<a name="anchor1"></a><br>

## Use of Uniform Resource Names 

An IOOS identifier is [Uniform Resource Identifier (URI)](https://www.ietf.org/rfc/rfc3986.txt). URIs are commonly used as identifiers in the Internet’s information architecture; an introductory description of URIs may be found on
[Wikipedia](http://en.wikipedia.org/wiki/Uniform_Resource_Identifier). In fact, IOOS identifiers are based on a specific form of URI, which is called a Uniform Resource Name (URN), which was designed for the identification of resources in particular namespaces. The URN syntax is described in the [Internet Engineering Task Force (IETF) Request for Comments (RFC) 2141](http://tools.ietf.org/html/rfc2141); the definitions and restrictions established by the RFC 2141 determine the syntactic structure of the IOOS identifiers.

All URIs assigned by IOOS begin with the string **`urn:ioos:`**, followed by one or more fields also separated by colons (`:`). The initial **`urn:`** indicates that the URI is indeed a URN. The following **`ioos:`** indicates that the URN is in the IOOS namespace.

_**NOTE**: The **`ioos`** namespace has not been formally registered with IANA; therefore, it is rather informal, community-wide namespace._

The additional fields may only include letters and numbers (_**A-Z**_, _**a-z**_, _**0-9**_) and the following characters: _**( ) + , - . = @ ; $ _ ! \***_

Special characters not in the foregoing list must be represented using hexadecimal encoding as _**%xx**_, where **xx** represents a two-digit hex value. The use of such characters in IOOS URNs is not recommended.

## Case-insensitivity

IOOS URNs are considered to be case-insensitive. The fields in IOOS URNs are customarily lower-case but may appear in UPPERCASE or MiXedCase. Example: `urn:ioos:ABC` and `urn:ioos:abc` refer to the same asset. This is more restrictive than the RFC 2141 provision; however, it is permitted.  

## Identifier Pattern

The general pattern for IOOS asset identifiers is

**`urn:ioos:asset_type:authority:label[:component][:discriminant][#functional_parameters]`**,

and encompasses of the following fields:

>**`urn:ioos`** (required) - a fixed string indicating this is an IOOS URN;

>**`asset_type`** (required) - a variable indicating the type of asset being identified;

>**`authority`** (required) - an abbreviation or name for the organization that assigned the label;

>**`label`** (required) - the number or label that was assigned by the authority to the asset;

>**`component`** (optional) - a name or ID of a specific component of a certain asset;

>**`discriminant`** (optional) - the component's sub-name for resolving duplicate components;

>**`functional_parameters`** - an extended metadata to represent various processes associated with the component.

The following sections explain in details the use of all the fields. The general requirement of the Convention is that the values of the fields have to be governed by a recognized controlled vocabulary; although some vocabularies are recommended hereinafter, other controlled vocabularies may be used as well.

### Asset Type

The **`asset_type`** field indicates the type of asset to which this identifier applies. The following values for **`asset_type`** are currently recognized by IOOS:

**glider**

>An autonomous vehicle that slowly (~20km/day) propels itself forward with very low power consumption by exploiting a controlled buoyancy in conjunction with wings and has a rudder for steering. Gliders either can autonomously navigate crossing large horizontal areas while vertically undulating the water column or can undulate at a near-fixed position acting as a virtual mooring.

**station**

>A fixed platform, installation, or nominally-constant position where measurements are performed.
Examples include: a water-level gauge mounted on a pier; a moored buoy that moves within a known watch radius of the nominal mooring location; an OceanSITES deep-water monitoring location; a site at which water quality samples are taken. 

**network**

>A network of stations defined above. 

**sensor**

>A device that detects or measures observed physical phenomena and records, indicates, or otherwise responds to it. Sensor typically is attached to a station or glider. 
Examples include: a water-level sensor; a temperature sensor; an anemometer; a current meter.<br>

**survey**

>A visual observation, measurement or collecting samples by a human observer performed at a station or from a ship for a follow-up analyses in the laboratory. Example: a quarterly visit to a known location to collect water for chemical analysis; an assessment by a diver of the species present in a particular location, etc.

Additional **`asset_type`** values may be added by IOOS as needed. The valid values in the **`asset_type`** field may be drawn from the following vocabularies or any other community-recognized controlled vocabulary:

* [Marine Metadata Initiative Device Ontology](http://mmisw.org/orr/#http://mmisw.org/ont/mmi/device)
* [BODC Instruments List](http://mmisw.org/orr/#http://vocab.ndg.nerc.ac.uk/list/L221/current)
* [GCMD Instrument types](http://gcmdservices.gsfc.nasa.gov/static/kms/instruments/instruments.csv)

### Authority

The **`authority`** field indicates the organization that assigned the label for this asset. There is no fixed set of values, because additional authorities may become relevant as new observing systems are connected to IOOS. However, the same abbreviation or name should be used for all instances of a particular authority. These abbreviations are case insensitive.  Here are a few examples of how the **`authority`** field is currently used in IOOS:

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

The valid values in the **`authority`** field may be drawn from the following vocabularies or any other community-recognized controlled vocabulary:

* GCMD Keywords
  * Data Centers: http://gcmdservices.gsfc.nasa.gov/static/kms/providers/providers.csv
  * Projects: http://gcmdservices.gsfc.nasa.gov/static/kms/projects/projects.csv

### Label

The **`label`** is a number or string assigned by the Authority to the asset. Allowed values are defined by the particular authority. The only restrictions are that 

 * the characters used must not conflict with the [URN specification](#anchor1), and
 * labels within the scope of a given authority must be unique.

### Component

The **`component`** field is used to label sub-assets in order to distinguish between different sub-assets associated with the same parent asset. The **`component`** value must be unique for each parent asset **`asset_type:authority:label`**.

### Discriminant

The **`discriminant`** field is a free-format text string that provides an additional means for resolving duplication of assets or sub-assets that may result from multiple deployments of the same asset, use of multiple identical sub-assets (e.g. sensors) at the same parent asset (e.g. station). The **`discriminant`** ensures the uniqueness of the multiple (sub-)asset's identifiers within the single asset's domain.<a name="anchor2"></a><br>

### Functional Parameters

The optional **`functional_parameters`** field provides extended metadata that depicts various processes associated with the component. Adding this metadata allows unambiguous identification of the data that is collected through the measurement of the identical phenomenon at the same station with different reference datums or post-processing methods. Although this field is not required, in cases like these it is the only way to identify the data that is normally impossible to represent without additional parameters. The functional parameters are especially valuable for conversing the netCDF attributes to IOOS SOS XML representation. 

Examples of the **`functional_parameters`** field values:

 - [Cell Methods](http://cfconventions.org/cf-conventions/v1.6.0/cf-conventions.html#cell-methods):
   - **`#cell_methods=time:mean;interval=pt24h`** (mean over time)
   - **`#cell_methods=time:standard_deviation`** (standard deviation)
 - [Vertical Datums](http://www.ngs.noaa.gov/datums/vertical/)
   - **`#vertical_datum=mllw`** (tidal MLLW datum)
   - **`#vertical_datum=navd88`** (geodetic datum NAVD 88)
   
Various parameters may be combined in one **`functional_parameters`** field, e.g.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **`#vertical_datum=mllw;cell_methods=time:mean;interval=pt12h`** (MLLW datum; mean over 12 hours processing)

# Convention for Specific Asset Types

## Station Identifiers

The pattern for IOOS platform (station) identifiers is 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **`urn:ioos:station:authority:label[:discriminant]`**. 

Station identifiers do not include a **`component`** field but may include a **`discriminant`** to identify, for example, a relocation of a mooring buoy or redeployment to the same location after sensor replacement.

## Glider Identifiers

The pattern for IOOS glider identifiers is similar to the station identifier

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **`urn:ioos:glider:authority:label[:discriminant]`**. 

As the same glider is typically associated with multiple deployments, the **`discriminant`** field in the glider's identifier adds unique information about each deployment like a deployment number, time, starting point coordinates, etc.; the complete identifier will allow unambiguous resolution of any of the glider's missions.

Since no field can contain a colon (**`":"`**), the date/time information cannot be reported in the ISO 8601 format, and  has to be provided in **YYYYmmddTHHMM** format, where **"YYYYmmdd"** depicts a deployment year, month and day, **"HHMM"** identifies a specific time, and **"T"** separates date and time fields, e.g. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **`urn:ioos:glider:edu.rutgers.marine:unit_191:20150105T1443`**. 

## Sensor Identifiers

For the purpose of this Convention, the sensors are always associated with a certain station, and are used to measure one or more observed quantities at or adjacent to the station location. The pattern for IOOS sensor identifiers is

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **`urn:ioos:sensor:authority:label:component[:discriminant][#functional_parameters]`**

The **`authority`** and **`label`** portions of the sensor's identifier are defined by the station the sensor is associated with; the **`component`** and **`discriminant`** fields combine into a unique sensor's name that distinguishes it from the other sensors at the same station. 

The **`component`** field may contain the make and model of the sensor (e.g., `SONTEK-ADP-419`), the phenomenon observed by that sensor (e.g., _`salinity`_), or an arbitrary label used by the organization that operates the sensor (e.g., `A1`). Whenever possible, the value from the [CF Standard Names](http://cfconventions.org/standard-names.html) table must be used as an observed property name (e.g., _`sea_water_temperature`_ rather than _`SeaTemp`_).

The **`discriminant`** field provides for unique identification of multiple sensors of the same type attached to the same platform for measuring the identical phenomenon, e.g. _`sea_water_temperature`_ or _`direction_of_sea_water_velocity`_ on different sides of the platform. Each sensor will have an identifier that includes the label for the platform and the label for the sensor; however, since the sensors and the observed properties are identical, it is impossible to distinguish one from another without providing additional information on the sensors such as sensor's location at the platform, time of deployment, serial number, etc. The resulting identifier will be perfectly unique within the platform:

 - **`urn:ioos:station:authority:label_station:sea_water_temperature:east`**, 
 - **`urn:ioos:station:authority:label_station:sea_water_temperature:bottom`**,
 - **`urn:ioos:station:authority:label_station:sea_water_temperature:nortek_adp_514`**

The **`functional_parameters`** field allows distinguishing of the measurements done by the same sensor but associated with different reference parameters or post-processing methods as described in the ["Functional Parameters"](#anchor2) section above.

## Survey Identifiers

A survey identifier URN shall include the **`authority`** and **`label`** fields of the station or a ship, and may include a **`component`** field to distinguish it from other surveys at the same station or ship:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **`urn:ioos:survey:authority:label[:component]`**

For visual observation purpose, the **`authority`**,  **`label`**, and **`component`** fields may also indicate either (1) the general observing protocol or (2) the specific type of observation.

### General observing protocol

If visual estimates are made according to some established observing protocol, then the **`authority`** field may contain a reference to the document that describes the protocol. For example, if observation was made by the [NWS Observing Handbook No. 1 (2004)](http://www.vos.noaa.gov/ObsHB-508/ObservingHandbook1_2004_508_compliant.pdf),
then the survey identifier will look as follows:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**`urn:ioos:survey:nws_observing_handbook_2004:label[:component]`**

If a simple reference to the document is sufficient to avoid any need for additional interpretation, it is acceptable to identify the survey with just the URL of the document describing the observing protocol, laboratory procedures, etc.
In the case of the NWS Observing Handbook, for example, the following URL may play a role of the survey ID:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**http://www.vos.noaa.gov/ObsHB-508/ObservingHandbook1_2004_508_compliant.pdf**

### Specific type of observation

The survey identifier may include the type of observation made by the human. For example, in the NWS Handbook, Chapter 2, page 2-7 says that "iw" is the "wind speed indicator", and that it has values 0, 1, 3, 4 depending on how the wind speed was estimated or measured, with "3" being "wind speed estimated in knots." For such an observation, the survey identifier may use the observation code instead of **`authority`**,  **`label`**, and **`component`** fields:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**`urn:ioos:survey:iw:3`**

or in a more verbose manner:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**`urn:ioos:survey:wind_speed_indicator:estimated_in_knots`**

Similarly, from p.2-76, sea surface temperature measurement can be identified as  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**`urn:ioos:survey:ss:1`**

or
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**`urn:ioos:survey:sst_indicator:negative_intake_measurement`**

