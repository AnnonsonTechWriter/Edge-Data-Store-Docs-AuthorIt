---
uid: sdsTypeProperty1-0
---

# SdsTypeProperty

The properties collection defines the fields in an SdsType.

The following table shows the required and optional SdsTypeProperty fields. Fields that are not included are reserved for internal SDS use.

|          Property         | Type                    | Optionality | Details |
|---------------------------|-------------------------|-------------|---------|
| Id                        | String                  | Required    | Identifier for referencing the type. |
| Name                      | String                  | Optional    | Friendly name. |
| Description               | String                  | Optional    | Description text. |
| SdsType                   | SdsType                 | Required    | Field defining the property's Type. |
| IsKey                     | Boolean                 | Required    | Identifies the property as the Key (Primary Index). |
| Value                     | Object                  | Optional    | Value of the property. |
| Order                     | Int                     | Optional    | Order of comparison within a compound index. |
| InterpolationMode         | SdsInterpolationMode    | Optional    | Interpolation setting of the property. Default is null. |
| Uom                       | String                  | Optional    | Unit of Measure of the property |

The SdsTypeProperty identifier follows the same rules as the SdsType identifier.

IsKey is a Boolean value used to identify the SdsType Key. A key defined by more than one property is called a compound key. The maximum number of properties that can define a compound key is three.

In a compound key, each property that is included in the key is specified as IsKey. The Order field defines the precedence of fields applied to the index.

The Value field is used for properties that represent a value. An example of a property with a value is an enum’s named constant. When representing an enum in a SdsType, the SdsType properties collection defines the enum’s constant list. The SdsTypeProperty Identifier represents the name of the constant and the SdsTypeProperty value represents the value of the constant (see the enum State definitions below).

InterpolationMode is assigned when the property of the event should be interpolated in a specific way that differs from the InterpolationMode of the SdsType. InterpolationMode is only applied to a property that is not part of the Index. If the InterpolationMode is not set, the property is are interpolated in the manner defined by the IntepolationMode of the SdsType.

An SdsType with the InterpolationMode set to ``Discrete`` cannot have a property with an InteroplationMode. For more information on interpolation of events, see [Interpolation](xref:sdsReadingData1-0#interpolation).

Uom is the unit of measure for the property. The Uom of a property may be specified by the name or the abbreviation. The names and abbreviations of Uoms are case sensitive.

The InterpolationMode and Uom of a property can be overridden on the stream. For more information, see [PropertyOverrides in Streams](xref:sdsStreams1-0#propertyoverrides).


## Supported units of measure

For a list of units of measures that are supported for an SdsTypeProperty, see [Units of measure](xref:SupportedUOM1-0).