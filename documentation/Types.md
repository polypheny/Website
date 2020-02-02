---
layout: page
title: Types
---

This page gives an overview about the data types supported by Polypheny.
	
### Bigint
8 bytes signed (two's complement). Ranges from `-9,223,372,036,854,775,808` to `+9,223,372,036,854,775,807`.
	
### Boolean
1-bit. Takes the value `true` and `false`. 
	
### Date
Represents a date. Format: `yyyy-mm-dd`
	
### Decimal
A decimal number is a number that can have a decimal point in it. The size argument has two parts: _precision_ and _scale_. The scale can not exceed the precision.
	
### Double
8 bytes IEEE 754. Covers a range from `4.94065645841246544e-324d` to `1.79769313486231570e+308d` (positive or negative). 
	
### Integer
4 bytes, signed (two's complement). Covers a range from `-2,147,483,648` to `2,147,483,647`. 
	
### Real
4 bytes, IEEE 754. Covers a range from `1.40129846432481707e-45` to `3.40282346638528860e+38` (positive or negative). 
	
### Text
String (can contain letters, numbers, and special characters) with variable length.
	
### Time
Represents a time of day without time zone. Format: `hh:mm:ss`
	
### Timestamp
Represents a combination of DATE and TIME values separated by a space. Format: `yyyy-mm-dd hh:mm:ss`

### Varbinary
Variable width binary string, the maximum length is specified in parenthesis.

### Varchar
String (can contain letters, numbers, and special characters) with variable length. The maximum length is specified in parenthesis.