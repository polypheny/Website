---
layout: page
title: Data Types
---

This page gives an overview about the data types supported by Polypheny.

* this unordered seed list will be replaced by toc as unordered list
{:toc}

## Scalar Types

| Type      | Description                                                                                                                                                                             |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| BIGINT    | 8 bytes signed (two's complement). Ranges from `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807`.                                                                             |
| BOOLEAN   | 1-bit. Takes the value `true` and `false`.                                                                                                                                              |
| DATE      | Represents a date. Format: `yyyy-mm-dd`                                                                                                                                                 |
| DECIMAL   | A decimal number is a number that can have a decimal point in it. This type has two arguments: _precision_ and _scale_. The scale can not exceed the precision.                         |
| DOUBLE    | 8 bytes IEEE 754. Covers a range from `4.94065645841246544e-324d` to `1.79769313486231570e+308d` (positive or negative).                                                                |
| INTEGER   | 4 bytes, signed (two's complement). Covers a range from `-2,147,483,648` to `2,147,483,647`.                                                                                            |
| REAL      | 4 bytes, IEEE 754. Covers a range from `1.40129846432481707e-45` to `3.40282346638528860e+38` (positive or negative).                                                                   |
| SMALLINT  | 2 bytes, signed (two's complement). Covers a range from `-32,768` to `32,767`.                                                                                                          |
| TIME      | Represents a time of day without time zone. Optionally, _precision_ can have a value between 0 and 3 specifying the number of fractional seconds. Format: `hh:mm:ss.f`                  |
| TIMESTAMP | Represents a combination of DATE and TIME values. Optionally,_precision_ can have a value between 0 and 3 specifying the number of fractional seconds. Format: `yyyy-mm-dd hh:mm:ss.f`  | 
| TINYINT   | 1 byte, signed (two's complement). Covers a range from `-128` to `127`.                                                                                                                 |
| VARCHAR   | String (can contain letters, numbers, and special characters) with variable length. The maximum length is specified as parameter.                                                       |


## Array Types

An array is an ordered, contiguous collection that may contain duplicates. Polypheny-DB 
supports arrays of all scalar types.

In Polypheny-DB, arrays can have an arbitrary _dimension_ and _cardinality_. Both are 
specified as arguments. Specifying -1 disables validation.

The _dimension_ specifies how deep arrays can be nested. A dimension of one therefore means
that nested arrays are not allowed while a dimension of two allows nested arrays but no 
nested arrays within nested arrays.

The _cardinality_ specifies the number of elements (values and nested arrays) in every 
(nested) array. 


## Multimedia and File Types

Polypheny-DB natively supports storing files. In addition to the generic `FILE` data type 
there are also additional types for multimedia content. Multimedia files are not checked 
by their file extension, but by their content type. 
See [SimpleMagic.ContentType](https://github.com/j256/simplemagic/blob/master/src/main/java/com/j256/simplemagic/ContentType.java) for more information.

| Type      | Description                                                                                                                                                       |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SOUND     | Accepted content types: _AIFF_, _AUDIO/MPEG_, _MIDI_, _REAL/AUDIO_, _WAV_                                                                                         |
| FILE      | Accepts files of any type.                                                                                                                                        |
| IMAGE     | Accepted content types: _APPLE_QUICKTIME_IMAGE_, _BMP_, _GIF_, _JPEG_, _JPEG 2000_, _PBM_, _PGM_, _PNG_, _PPM_, _SVG_, _TIFF_                                     |
| VIDEO     | Accepted content types: _APPLE_QUICKTIME_MOVIE_, _AVI_, _MNG_, _MP4A_, _MP4V_, _VIDEO/MPEG_                                                                       |

