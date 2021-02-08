---
layout: plain
title: Schema Model
---

Polypheny has a two level hierarchical schema model. The first level consists of schemas. A schema is a namespace that contains named database objects such as tables and views.

To access an object in a schema, you need to qualify the object by using the following syntax:
{% highlight sql %}
schemaName.objectName
{% endhighlight %}

Two schemas can have different objects that share the same name.

Polypheny automatically creates a schema called `public`. Whatever object you create without specifying the schema name, Polypheny will place it into this `public` schema.