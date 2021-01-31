---
layout: page
title: CSV Adapter
---

The CSV data source adapter allows to query CSV files as relational tables. Please make sure that the first line of your CSV files contains a header according to the specification bellow.  The adapter supports multiple CSV files. Every file is represented as a table using the filename as table name. Make sure that the file name contains no spaces. The adapter also supports files compressed using gzip. The file name must either end with `.csv` or `.csv.gz`.

The CSV adapter is read-only. DML queries are not supported. The content of the file can be changed as long as the schema (number of columns and there type) is not changed.


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
{% endhighlight %}


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
| string    | String (can contain letters, numbers, and special characters). Wrapped in double quotes if containing commas. Mapped to a VARCHAR. Length can be specified using the adapter parameter `maxStringLength`.  |
| time      | Format: `hh:mm:ss` No support for fractional seconds.                                                                                                             |
| timestamp | Format: `yyyy-mm-dd hh:mm:ss` No support for fractional seconds.                                                                                                  | 


## Example

{% highlight csv %}
id:long,name:string,level:int,birthday:date,fulltime:boolean,start:time,last_update:timestamp,tfloat:float,tdouble:double
1,Alice,9,1992-11-14,true,08:00:00,2021-01-30 13:30:04+00:00,1.999,2.333
2,"Hans Wurst",6,1989-08-01,0,08:15:00,2020-11-01 09:05:12.111,0.1,999.999999
{% endhighlight %}


## Deployment

The adapter can either be deployed using the Polypheny-UI (Adapters -> Sources) or using the following SQL statement:

{% highlight sql %}
ALTER ADAPTERS ADD uniqueName USING 'org.polypheny.db.adapter.csv.CsvSource' WITH '{directory:"csvFolder",maxStringLength:"255"}'
{% endhighlight %}

Please make sure to adjust `csvFolder` and the `maxStringLength` according to your needs.

After successful deployment, all CSV files are mapped as a table in the public schema. The tables and columns can be renamed. Furthermore, columns can be reordered and dropped if they are not required (they are not deleted from the file). If you have changed your mind, dropped columns can be added again using the Polypheny-UI or this special SQL statement:

{% highlight sql %}
ALTER TABLE tableName ADD COLUMN physicalName AS name
{% endhighlight %}

`physicalName` referes to the name specified in the header of the CSV file. 
