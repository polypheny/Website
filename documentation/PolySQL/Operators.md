---
layout: page
title: Operators and Functions
---

This page outlines the available SQL operators and functions supported by Polypheny-DB.

* this unordered seed list will be replaced by toc as unordered list
{:toc}

### Operator precedence

The operator precedence and associativity, highest to lowest.

| Operator                                          | Associativity
|:------------------------------------------------- |:-------------
| .                                                 | left
| [ ] (array element)                               | left
| + - (unary plus, minus)                           | right
| * / %                                             | left
| + -                                               | left
| BETWEEN, IN, LIKE, SIMILAR, OVERLAPS, CONTAINS etc. | -
| < > = <= >= <> !=                                 | left
| IS NULL, IS FALSE, IS NOT TRUE etc.               | -
| NOT                                               | right
| AND                                               | left
| OR                                                | left


### Comparison operators

| Operator syntax                                   | Description
|:------------------------------------------------- |:-----------
| value1 = value2                                   | Equals
| value1 <> value2                                  | Not equal
| value1 != value2                                  | Not equal (only available at some conformance levels)
| value1 > value2                                   | Greater than
| value1 >= value2                                  | Greater than or equal
| value1 < value2                                   | Less than
| value1 <= value2                                  | Less than or equal
| value IS NULL                                     | Whether *value* is null
| value IS NOT NULL                                 | Whether *value* is not null
| value1 IS DISTINCT FROM value2                    | Whether two values are not equal, treating null values as the same
| value1 IS NOT DISTINCT FROM value2                | Whether two values are equal, treating null values as the same
| value1 BETWEEN value2 AND value3                  | Whether *value1* is greater than or equal to *value2* and less than or equal to *value3*
| value1 NOT BETWEEN value2 AND value3              | Whether *value1* is less than *value2* or greater than *value3*
| string1 LIKE string2 [ ESCAPE string3 ]           | Whether *string1* matches pattern *string2*
| string1 NOT LIKE string2 [ ESCAPE string3 ]       | Whether *string1* does not match pattern *string2*
| string1 SIMILAR TO string2 [ ESCAPE string3 ]     | Whether *string1* matches regular expression *string2*
| string1 NOT SIMILAR TO string2 [ ESCAPE string3 ] | Whether *string1* does not match regular expression *string2*
| value IN (value [, value]*)                       | Whether *value* is equal to a value in a list
| value NOT IN (value [, value]*)                   | Whether *value* is not equal to every value in a list
| value IN (sub-query)                              | Whether *value* is equal to a row returned by *sub-query*
| value NOT IN (sub-query)                          | Whether *value* is not equal to every row returned by *sub-query*
| value comparison SOME (sub-query)                 | Whether *value* *comparison* at least one row returned by *sub-query*
| value comparison ANY (sub-query)                  | Synonym for SOME
| value comparison ALL (sub-query)                  | Whether *value* *comparison* every row returned by *sub-query*
| EXISTS (sub-query)                                | Whether *sub-query* returns at least one row

{% highlight sql %}
comp:
      =
  |   <>
  |   >
  |   >=
  |   <
  |   <=
{% endhighlight %}


### Logical operators

| Operator syntax        | Description
|:---------------------- |:-----------
| boolean1 OR boolean2   | Whether *boolean1* is TRUE or *boolean2* is TRUE
| boolean1 AND boolean2  | Whether *boolean1* and *boolean2* are both TRUE
| NOT boolean            | Whether *boolean* is not TRUE;
| boolean IS FALSE       | Whether *boolean* is FALSE;
| boolean IS NOT FALSE   | Whether *boolean* is not FALSE;
| boolean IS TRUE        | Whether *boolean* is TRUE;
| boolean IS NOT TRUE    | Whether *boolean* is not TRUE;


### Arithmetic operators and functions

| Operator syntax           | Description
|:------------------------- |:-----------
| + numeric                 | Returns *numeric*
| - numeric                 | Returns negative *numeric*
| numeric1 + numeric2       | Returns *numeric1* plus *numeric2*
| numeric1 - numeric2       | Returns *numeric1* minus *numeric2*
| numeric1 * numeric2       | Returns *numeric1* multiplied by *numeric2*
| numeric1 / numeric2       | Returns *numeric1* divided by *numeric2*
| numeric1 % numeric2       | As *MOD(numeric1, numeric2)* 
| POWER(numeric1, numeric2) | Returns *numeric1* raised to the power of *numeric2*
| ABS(numeric)              | Returns the absolute value of *numeric*
| MOD(numeric1, numeric2)   | Returns the remainder (modulus) of *numeric1* divided by *numeric2*. The result is negative only if *numeric1* is negative
| SQRT(numeric)             | Returns the square root of *numeric*
| LN(numeric)               | Returns the natural logarithm (base *e*) of *numeric*
| LOG10(numeric)            | Returns the base 10 logarithm of *numeric*
| EXP(numeric)              | Returns *e* raised to the power of *numeric*
| CEIL(numeric)             | Rounds *numeric* up, returning the smallest integer that is greater than or equal to *numeric*
| FLOOR(numeric)            | Rounds *numeric* down, returning the largest integer that is less than or equal to *numeric*
| RAND([seed])              | Generates a random double between 0 and 1 inclusive, optionally initializing the random number generator with *seed*
| RAND_INTEGER([seed, ] numeric) | Generates a random integer between 0 and *numeric* - 1 inclusive, optionally initializing the random number generator with *seed*
| ACOS(numeric)             | Returns the arc cosine of *numeric*
| ASIN(numeric)             | Returns the arc sine of *numeric*
| ATAN(numeric)             | Returns the arc tangent of *numeric*
| ATAN2(numeric, numeric)   | Returns the arc tangent of the *numeric* coordinates
| COS(numeric)              | Returns the cosine of *numeric*
| COT(numeric)              | Returns the cotangent of *numeric*
| DEGREES(numeric)          | Converts *numeric* from radians to degrees
| PI()                      | Returns a value that is closer than any other value to *pi*
| RADIANS(numeric)          | Converts *numeric* from degrees to radians
| ROUND(numeric1 [, numeric2]) | Rounds *numeric1* to optionally *numeric2* (if not specified 0) places right to the decimal point
| SIGN(numeric)             | Returns the signum of *numeric*
| SIN(numeric)              | Returns the sine of *numeric*
| TAN(numeric)              | Returns the tangent of *numeric*
| TRUNCATE(numeric1 [, numeric2]) | Truncates *numeric1* to optionally *numeric2* (if not specified 0) places right to the decimal point
| distance(array1, array2, metric) | See [knn Search](KNN.md) for details.
| distance(array1, array2, metric, weights) | See [knn Search](KNN.md) for details.


### Character string operators and functions

| Operator syntax            | Description
|:-------------------------- |:-----------
| string &#124;&#124; string | Concatenates two character strings
| CHAR_LENGTH(string)        | Returns the number of characters in a character string
| CHARACTER_LENGTH(string)   | Alias for CHAR_LENGTH(*string*)
| UPPER(string)              | Returns a character string converted to upper case
| LOWER(string)              | Returns a character string converted to lower case
| POSITION(string1 IN string2) | Returns the position of the first occurrence of *string1* in *string2*
| POSITION(string1 IN string2 FROM integer) | Returns the position of the first occurrence of *string1* in *string2* starting at a given point (not standard SQL)
| TRIM( { BOTH &#124; LEADING &#124; TRAILING } string1 FROM string2) | Removes the longest string containing only the characters in *string1* from the start/end/both ends of *string1*
| OVERLAY(string1 PLACING string2 FROM integer [ FOR integer2 ]) | Replaces a substring of *string1* with *string2*
| SUBSTRING(string FROM integer)  | Returns a substring of a character string starting at a given point
| SUBSTRING(string FROM integer FOR integer) | Returns a substring of a character string starting at a given point with a given length
| INITCAP(string)            | Returns *string* with the first letter of each word converter to upper case and the rest to lower case. Words are sequences of alphanumeric characters separated by non-alphanumeric characters.


### Date/time functions

| Operator syntax           | Description
|:------------------------- |:-----------
| LOCALTIME                 | Returns the current time in the session time zone in a value of datatype TIME, with three digits of precision.
| LOCALTIME(precision)      | Returns the current time in the session time zone in a value of datatype TIME, with *precision* digits of precision.
| LOCALTIMESTAMP            | Returns the current date and time in the session time zone in a value of datatype TIMESTAMP, with three digits of precision.
| LOCALTIMESTAMP(precision) | Returns the current date and time in the session time zone in a value of datatype TIMESTAMP, with *precision* digits of precision.
| CURRENT_TIME              | Alias for LOCALTIME.
| CURRENT_DATE              | Returns the current date in the session time zone, in a value of datatype DATE.
| CURRENT_TIMESTAMP         | Alias for LOCALTIMESTAMP.
| EXTRACT(timeUnit FROM timestamp) | Extracts and returns the value of a specified timestamp field from a timestamp value expression.
| FLOOR(timestamp TO timeUnit) | Rounds *timestamp* down to *timeUnit*.
| CEIL(timestamp TO timeUnit) | Rounds *timestamp* up to *timeUnit*.
| YEAR(date)                | Equivalent to `EXTRACT(YEAR FROM date)`. Returns an integer.
| QUARTER(date)             | Equivalent to `EXTRACT(QUARTER FROM date)`. Returns an integer between 1 and 4.
| MONTH(date)               | Equivalent to `EXTRACT(MONTH FROM date)`. Returns an integer between 1 and 12.
| WEEK(date)                | Equivalent to `EXTRACT(WEEK FROM date)`. Returns an integer between 1 and 53.
| DAYOFYEAR(date)           | Equivalent to `EXTRACT(DOY FROM date)`. Returns an integer between 1 and 366.
| DAYOFMONTH(date)          | Equivalent to `EXTRACT(DAY FROM date)`. Returns an integer between 1 and 31.
| DAYOFWEEK(date)           | Equivalent to `EXTRACT(DOW FROM date)`. Returns an integer between 1 and 7.
| HOUR(date)                | Equivalent to `EXTRACT(HOUR FROM date)`. Returns an integer between 0 and 23.
| MINUTE(date)              | Equivalent to `EXTRACT(MINUTE FROM date)`. Returns an integer between 0 and 59.
| SECOND(date)              | Equivalent to `EXTRACT(SECOND FROM date)`. Returns an integer between 0 and 59.
| TIMESTAMPADD(timeUnit, integer, timestamp) | Returns *timestamp* with an interval of (signed) *integer* *timeUnit*s added.
| TIMESTAMPDIFF(timeUnit, timestamp, timestamp2) | Returns the (signed) number of *timeUnit* intervals between *timestamp* and *timestamp2*. Equivalent to `(timestamp2 - timestamp) timeUnit`

Calls to niladic functions such as `CURRENT_DATE` do not accept parentheses in
standard SQL. Calls with parentheses, such as `CURRENT_DATE()` are accepted in certain
[conformance levels]({{ site.apiRoot }}/org/polypheny/db/sql/validate/SqlConformance.html#allowNiladicParentheses--).


### System functions

| Operator syntax | Description
|:--------------- |:-----------
| USER            | Equivalent to CURRENT_USER
| CURRENT_USER    | User name of current execution context
| SESSION_USER    | Session user name
| SYSTEM_USER     | Returns the name of the current data store user as identified by the operating system


### Conditional functions and operators

| Operator syntax | Description
|:--------------- |:-----------
| CASE value<br/>WHEN value1 [, value11 ]* THEN result1<br/>[ WHEN valueN [, valueN1 ]* THEN resultN ]*<br/>[ ELSE resultZ ]<br/> END | Simple case
| CASE<br/>WHEN condition1 THEN result1<br/>[ WHEN conditionN THEN resultN ]*<br/>[ ELSE resultZ ]<br/>END | Searched case
| NULLIF(value, value) | Returns NULL if the values are the same.<br/><br/>For example, <code>NULLIF(5, 5)</code> returns NULL; <code>NULLIF(5, 0)</code> returns 5.
| COALESCE(value, value [, value ]*) | Provides a value if the first value is null.<br/><br/>For example, <code>COALESCE(NULL, 5)</code> returns 5.


### Type conversion

| Operator syntax | Description
|:--------------- | :----------
| CAST(value AS type) | Converts a value to a given type.


### Value constructors

| Operator syntax | Description
|:--------------- |:-----------
| ROW (value [, value ]*)  | Creates a row from a list of values.
| (value [, value ]* )     | Creates a row from a list of values.
| array '[' index ']' | Returns the element at a particular location in an array.
| ARRAY '[' value [, value ]* ']' | Creates an array from a list of values.


<br>
_Parts of this documentation are based on [Calcite SQL Reference](https://calcite.apache.org/docs/reference.html)._