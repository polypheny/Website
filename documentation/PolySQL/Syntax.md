---
layout: plain
title: PolySQL Syntax
---

The page describes the SQL dialect recognized by Polypheny-DB's default SQL parser in a [BNF](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_Form)-like form.

{% highlight sql %}
statement:
      insert
  |   update
  |   delete
  |   query

insert:
      INSERT INTO tableName
      [ '(' column [, column ]* ')' ]
      query

update:
      UPDATE tableName
      SET assign [, assign ]*
      [ WHERE booleanExpression ]

assign:
      identifier '=' expression

delete:
      DELETE FROM tableName [ [ AS ] alias ]
      [ WHERE booleanExpression ]

query:
      values
  |   WITH withItem [ , withItem ]* query
  |   {
          select
      |   selectWithoutFrom
      |   query UNION [ ALL | DISTINCT ] query
      |   query EXCEPT [ ALL | DISTINCT ] query
      |   query MINUS [ ALL | DISTINCT ] query
      |   query INTERSECT [ ALL | DISTINCT ] query
      }
      [ ORDER BY orderItem [, orderItem ]* ]
      [ LIMIT [ start, ] { count | ALL } ]
      [ OFFSET start { ROW | ROWS } ]
      [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]

withItem:
      name
      [ '(' column [, column ]* ')' ]
      AS '(' query ')'

orderItem:
      expression [ ASC | DESC ] [ NULLS FIRST | NULLS LAST ]

select:
      SELECT [ STREAM ] [ ALL | DISTINCT ]
          { * | projectItem [, projectItem ]* }
      FROM tableExpression
      [ WHERE booleanExpression ]
      [ GROUP BY { groupItem [, groupItem ]* } ]
      [ HAVING booleanExpression ]
      [ WINDOW windowName AS windowSpec [, windowName AS windowSpec ]* ]

selectWithoutFrom:
      SELECT [ ALL | DISTINCT ]
          { * | projectItem [, projectItem ]* }

projectItem:
      expression [ [ AS ] columnAlias ]
  |   tableAlias . *

tableExpression:
      tableReference [, tableReference ]*
  |   tableExpression [ NATURAL ] [ ( LEFT | RIGHT | FULL ) [ OUTER ] ] JOIN tableExpression [ joinCondition ]
  |   tableExpression CROSS JOIN tableExpression
  |   tableExpression [ CROSS | OUTER ] APPLY tableExpression

joinCondition:
      ON booleanExpression
  |   USING '(' column [, column ]* ')'

tableReference:
      tableName
      [ matchRecognize ]
      [ [ AS ] alias [ '(' columnAlias [, columnAlias ]* ')' ] ]

tableName:
      [ schemaName . ] tableName
      '(' TABLE [ schemaName . ] tableName ')'
  |   tableName [ EXTEND ] '(' columnDecl [, columnDecl ]* ')'
  |   [ LATERAL ] '(' query ')'
  |   UNNEST '(' expression ')' [ WITH ORDINALITY ]
  |   [ LATERAL ] TABLE '(' [ SPECIFIC ] functionName '(' expression [, expression ]* ')' ')'

columnDecl:
      column type [ NOT NULL ]

values:
      VALUES expression [, expression ]*

groupItem:
      expression
  |   '(' ')'
  |   '(' expression [, expression ]* ')'
  |   CUBE '(' expression [, expression ]* ')'
  |   ROLLUP '(' expression [, expression ]* ')'
  |   GROUPING SETS '(' groupItem [, groupItem ]* ')'

windowRef:
      windowName
  |   windowSpec

windowSpec:
      [ windowName ]
      '('
      [ ORDER BY orderItem [, orderItem ]* ]
      [ PARTITION BY expression [, expression ]* ]
      [
          RANGE numericOrIntervalExpression { PRECEDING | FOLLOWING }
      |   ROWS numericExpression { PRECEDING | FOLLOWING }
      ]
      ')'
{% endhighlight %}


In *insert*, if the INSERT statement does not specify a list of target columns, the query must have the same number of columns as the target table.

In *orderItem*, if *expression* is a positive integer *n*, it denotes the <em>n</em>th item in the SELECT clause.

In *query*, *count* and *start* may each be either an unsigned integer literal or a dynamic parameter whose value is an integer.

An aggregate query is a query that contains a GROUP BY or a HAVING clause, or aggregate functions in the SELECT clause. In the SELECT, HAVING and ORDER BY clauses of an aggregate query, all expressions must be constant within the current group (that is, grouping constants as defined by the GROUP BY clause, or constants), or aggregate functions, or a combination of constants and aggregate functions. Aggregate and grouping functions may only appear in an aggregate query, and only in a SELECT, HAVING or ORDER BY clause.

A scalar sub-query is a sub-query used as an expression. If the sub-query returns no rows, the value is NULL; if it returns more than one row, it is an error.

IN, EXISTS and scalar sub-queries can occur in any place where an expression can occur (such as the SELECT clause, WHERE clause, ON clause of a JOIN, or as an argument to an aggregate function).

An IN, EXISTS or scalar sub-query may be correlated; that is, it may refer to tables in the FROM clause of an enclosing query.

*selectWithoutFrom* is equivalent to VALUES.

MINUS is equivalent to EXCEPT.

"LIMIT start, count" is equivalent to "LIMIT count OFFSET start".


<br>
_Parts of this documentation are based on [Calcite SQL Reference](https://calcite.apache.org/docs/reference.html)._