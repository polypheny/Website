---
layout: page
title: Types
---

This page gives an overview about the data types supported by Polypheny.

## Scalar types

| Type      | Description                                                                                                                                                       |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Bigint    | 8 bytes signed (two's complement). Ranges from `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807`.                                                       |
| Boolean   | 1-bit. Takes the value `true` and `false`.                                                                                                                        |
| Date      | Represents a date. Format: `yyyy-mm-dd`                                                                                                                           |
| Decimal   | A decimal number is a number that can have a decimal point in it. This type has two arguments: _precision_ and _scale_. The scale can not exceed the precision.   |
| Double    | 8 bytes IEEE 754. Covers a range from `4.94065645841246544e-324d` to `1.79769313486231570e+308d` (positive or negative).                                          |
| Integer   | 4 bytes, signed (two's complement). Covers a range from `-2,147,483,648` to `2,147,483,647`.                                                                      |
| Real      | 4 bytes, IEEE 754. Covers a range from `1.40129846432481707e-45` to `3.40282346638528860e+38` (positive or negative).                                             |
| Smallint  | 2 bytes, signed (two's complement). Covers a range from `-32,768` to `32,767`.                                                                                    |
| Time      | Represents a time of day without time zone. Can optionally be defined with a fractional second _precision_ between 0 and 3. Format: `hh:mm:ss.f`                  |
| Timestamp | Represents a combination of DATE and TIME values. Can optionally be defined with a fractional second _precision_ between 0 and 3. Format: `yyyy-mm-dd hh:mm:ss.f` | 
| Tinyint   | 1 byte, signed (two's complement). Covers a range from `-128` to `127`.                                                                                           |
| Varchar   | String (can contain letters, numbers, and special characters) with variable length. The maximum length is specified as parameter.                                 |


## Array types

An array is an ordered, contiguous collection that may contain duplicates. Polypheny-DB 
supports arrays of all scalar types.

In Polypheny-DB, arrays can have an arbitrary _dimension_ and _cardinality_. Both are 
specified as arguments. Specifying -1 disables validation.

The _dimension_ specifies how deep arrays can be nested. A dimension of one therefore means
that nested arrays are not allowed while a dimension of two allows nested arrays but no 
nested arrays within nested arrays.

The _cardinality_ specifies the number of elements (values and nested arrays) in every 
(nested) array. 

