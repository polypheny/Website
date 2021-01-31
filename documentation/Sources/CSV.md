---
layout: page
title: CSV Adapter
---

The CSV data source adapter allows to query CSV files as relational tables. Please make sure that the first line of your CSV files contains a header according to the specification bellow.  The adapter supports multiple CSV files. Every file is represented as a table using the filename as table name. Make sure that the file name contains no spaces. The adapter also supports files compressed using gzip. The file name must either end with '.csv' or '.csv.gz'.


## Adapter Settings

The CSV adapter has to settings: 
| Setting         | Description                                                                                                                                                       |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| directory       | The location of the directory containing the CSV files.                                                                                                           |
| maxStringLength | Which length (number of characters including whitespace) should be used for the varchar columns. Make sure this is equal or larger than your longest string in any of the columns. |


## File Header
The first line of the CSV file needs to contain a header specifying the name and data type of every column. The column name and the data type need to be separated by a colon:

{% highlight csv %}
id:int,name:string
1,Alice
{% endhighlight %}

The name is used as initial column name and can be changed.


## Supported Data Types
The CSV adapter supports the following data types:

| Type      | Description                                                                                                                                                       |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| boolean   | Allowed values: `true`, `false`, `0` and `1`.                                                                                                                     |
| date      | Format: `yyyy-mm-dd`                                                                                                                                              |
| double    | Floating point number using a '.' (dot) as decimal separator. Mapped to the data type DOUBLE (8 bytes, IEEE 754).                                                 |
| float     | Floating point number using a '.' (dot) as decimal separator. Mapped to the data type REAL (4 bytes, IEEE 754).                                                   |
| int       | Integer number in the range `-2,147,483,648` to `2,147,483,647`.                                                                                                  |
| long      | Integer number in the range `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807`. Mapped to the data type BIGINT                                           |
| string    | String (can contain letters, numbers, and special characters). Wrapped in double quotes if containing commas. Mapped to a VARCHAR. Length can be specified using the adapter parameter `maxStringLength` (Default: 255)   |
| time      | Format: `hh:mm:ss` No support for fractional seconds.                                                                                                             |
| timestamp | Format: `yyyy-mm-dd hh:mm:ss` No support for fractional seconds.                                                                                                  | 


Example:

{% highlight csv %}
id:long,name:string,level:int,birthday:date,fulltime:boolean,start:time,last_update:timestamp,tfloat:float,tdouble:double
1,Alice,9,1992-11-14,true,08:00:00,2021-01-30 13:30:04+00:00,1.999,2.333
2,"Hans Wurst",6,1989-08-01,0,08:15:00,2020-11-01 09:05:12.111,0.1,999.999999
{% endhighlight %}



