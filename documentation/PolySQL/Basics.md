---
layout: plain
title: Basics
---

This page gives an basic overview on PolySQL, the SQL dialect of Polypheny.


## Identifiers

Identifiers are the names of tables, columns, indexes and other metadata elements used in a query. Identifiers must start with a letter and can only contain letters, digits, and underscores. They are implicitly converted to lower case.

If an identifier name clashes with a reserved keyword, the name needs to be quoted. Quoted identifiers, such as `"user"`, start and end with double quotes.


## Strings

Strings need to be embedded in single quotes (`'`). To use a single quote within a string, it must be escaped by doubling it. Example:
{% highlight sql %}
INSERT INTO test VALUES (1, 'A single quote '' needs to be doubled')
{% endhighlight %}

This will insert the string:
{% highlight sql %}
A single quote ' needs to be doubled
{% endhighlight %}