---
layout: plain
title: Schema Manipulation
---

Overview on the available statements for defining and altering the schema in a [BNF](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_Form)-like form.

{% highlight sql %}
statement:
      alterStatement
  |   createSchemaStatement
  |   createTableStatement
  |   dropSchemaStatement
  |   dropTableStatement
  |   truncateTableStatement

createSchemaStatement:
      CREATE [ OR REPLACE ] SCHEMA [ IF NOT EXISTS ] name

createTableStatement:
      CREATE TABLE [ IF NOT EXISTS ] name
      [ '(' tableElement [, tableElement ]* ')' ]
      [ ON STORE store ]
      [ PARTITION BY ( HASH | RANGE | LIST ) '(' columnName ')' [PARTITIONS numberPartitions | with (partitionName1, partitionName2 [, partitionNameN]* )] ]

tableElement:
      columnName type [ NOT ] NULL [ DEFAULT value ]
  |   PRIMARY KEY '(' columnName [, columnName ]* ')'
  |   UNIQUE '(' columnName [, columnName ]* ')'
     

dropSchemaStatement:
      DROP SCHEMA [ IF EXISTS ] name

dropTableStatement:
      DROP TABLE [ IF EXISTS ] name
      
truncateTableStatement:
      TRUNCATE TABLE name

alterStatement:
       ALTER SCHEMA schemaName RENAME TO newSchemaName  
     | ALTER SCHEMA schemaName OWNER TO userName  
     | ALTER TABLE [ schemaName . ] tableName RENAME TO newTableName  
     | ALTER TABLE [ schemaName . ] tableName OWNER TO userName
     | ALTER TABLE [ schemaName . ] tableName RENAME COLUMN columnName TO newColumnName
     | ALTER TABLE [ schemaName . ] tableName DROP COLUMN columnName
     | ALTER TABLE [ schemaName . ] tableName ADD COLUMN columnName type [ NULL | NOT NULL ] [DEFAULT defaultValue] [(BEFORE | AFTER) columnName]
     | ALTER TABLE [ schemaName . ] tableName ADD COLUMN columnName physicalName AS name [DEFAULT defaultValue] [(BEFORE | AFTER) columnName]
     | ALTER TABLE [ schemaName . ] tableName MODIFY COLUMN columnName SET NOT NULL
     | ALTER TABLE [ schemaName . ] tableName MODIFY COLUMN columnName DROP NOT NULL
     | ALTER TABLE [ schemaName . ] tableName MODIFY COLUMN columnName SET COLLATION collation
     | ALTER TABLE [ schemaName . ] tableName MODIFY COLUMN columnName SET DEFAULT value
     | ALTER TABLE [ schemaName . ] tableName MODIFY COLUMN columnName DROP DEFAULT
     | ALTER TABLE [ schemaName . ] tableName MODIFY COLUMN columnName SET TYPE type
     | ALTER TABLE [ schemaName . ] tableName MODIFY COLUMN columnName SET POSITION ( BEFORE | AFTER ) columnName
     | ALTER TABLE [ schemaName . ] tableName ADD PRIMARY KEY ( columnName | '(' columnName [ , columnName ]* ')' )
     | ALTER TABLE [ schemaName . ] tableName DROP PRIMARY KEY
     | ALTER TABLE [ schemaName . ] tableName ADD CONSTRAINT constraintName UNIQUE ( columnName| '(' columnName [ , columnName ]* ')' )
     | ALTER TABLE [ schemaName . ] tableName DROP CONSTRAINT constraintName
     | ALTER TABLE [ schemaName . ] tableName ADD CONSTRAINT foreignKeyName FOREIGN KEY ( columnName | '(' columnName [ , columnName ]* ')' ) REFERENCES [ schemaName . ] tableName '(' columnName [ , columnName ]* ')' [ ON UPDATE ( CASCADE | RESTRICT | SET NULL | SET DEFAULT ) ] [ ON DELETE ( CASCADE | RESTRICT | SET NULL | SET DEFAULT ) ]
     | ALTER TABLE [ schemaName . ] tableName DROP FOREIGN KEY foreignKeyName
     | ALTER TABLE [ schemaName . ] tableName ADD [UNIQUE] INDEX indexName ON ( columnName | '(' columnName [ , columnName ]* ')' ) [ USING indexMethod ] [ ON STORE storeUniqueName ]
     | ALTER TABLE [ schemaName . ] tableName DROP INDEX indexName
     | ALTER TABLE [ schemaName . ] tableName ADD PLACEMENT [( columnName | '(' columnName [ , columnName ]* ')' )] ON STORE storeUniqueName [ WITH PARTITIONS '(' partitionName [ , partitionName ]* ')' ]
     | ALTER TABLE [ schemaName . ] tableName MODIFY PLACEMENT ( ADD | DROP ) COLUMN columnName ON STORE storeUniqueName
     | ALTER TABLE [ schemaName . ] tableName MODIFY PLACEMENT '(' columnName [ , columnName ]* ')' ON STORE storeUniqueName [ WITH PARTITIONS '(' partitionName [ , partitionName ]* ')' ]
     | ALTER TABLE [ schemaName . ] tableName DROP PLACEMENT ON STORE storeUniqueName
     | ALTER TABLE [ schemaName . ] tableName PARTITION BY ( HASH | RANGE | LIST) '(' columnName ')' [ PARTITIONS numPartitions | WITH '(' partitionName1, partitionName2 [, partitionNameN]* ')' ]
     | ALTER TABLE [ schemaName . ] tableName MERGE PARTITIONS
     | ALTER TABLE [ schemaName . ] tableName MODIFY PARTITIONS '(' partitionId [ , partitionId ]* ')' ON STORE storeUniqueName
{% endhighlight %}