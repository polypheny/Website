---
layout: plain
title: System Management
---

Polypheny puts the concept of polyglot persistence on a new level by allowing not only allowing to query and manipulate data using different languages but also managing the system. This page gives an overview on available commands for managing the system using special DDL statements.

* this unordered seed list will be replaced by toc as unordered list
{:toc}


## Altering config values

It is possible to change the value of configuration settings using the following PolySQL statement:

{% highlight sql %}
ALTER CONFIG key SET value
{% endhighlight %}

The `key` refers to the name of the configuration to be changed. The following example shows how to disable the query implementation caching:

{% highlight sql %}
ALTER CONFIG 'runtime/implementationCaching' SET false
{% endhighlight %}



## Adding adapters

Adapters (Data Sources and Data Stores) can be deployed using the following PolySQL statement:

{% highlight sql %}
ALTER ADAPTERS ADD uniqueName USING adapterClass WITH config 
{% endhighlight %}

The `uniqueName` is the identifier to be used for the data store or data source and must be unique. `adapterClass` needs to be a string containing the qualified class name of the adapter implementation to be used. The values for the available parameters of the adapter are specified by `config` as a JSON string containing key-value pairs. 

The following example shows a statement for deploying a CSV source adapter:

{% highlight sql %}
ALTER ADAPTERS ADD foo USING 'org.polypheny.db.adapter.csv.CsvSource' WITH '{directory:"csvFolder",maxStringLength:"255"}'
{% endhighlight %}



## Dropping adapters

Adapters (Data Sources and Data Stores) can be removed using the following PolySQL statement:

{% highlight sql %}
ALTER ADAPTERS DROP uniqueName
{% endhighlight %}

`uniqueName` refers to the identifier of the data store or data source to be removed.


## Adding query interfaces

It is possible to add query interfaces using the following PolySQL statement:

{% highlight sql %}
ALTER INTERFACES ADD uniqueName USING clazzName WITH config
{% endhighlight %}

The `uniqueName` is the identifier to be used for the query interface and needs to be unique. `clazzName` specifies the qualified class name of the query interface implementation to be deployed. The `config` is a JSON string containing key-value pairs for the parameters of the query interface. 

The following example shows a statement for deploying a REST query interface:

{% highlight sql %}
ALTER INTERFACES ADD foo USING 'org.polypheny.db.restapi.HttpRestServer' WITH '{port:"8089",maxUploadSizeMb:"10000"}'
{% endhighlight %}



## Dropping query interfaces

Query interfaces can be removed using the following PolySQL statement:

{% highlight sql %}
ALTER INTERFACES DROP uniqueName
{% endhighlight %}

`uniqueName` refers to the identifier of the query interface to be removed.

