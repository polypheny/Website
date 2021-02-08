---
title:  k-Nearest-Neighbor Search
description: >
  How to use k-nearest-neighbour search in Polypheny.
hide_description: true
---

k-nearest-neighbour search functionality is a way to find entries based on their distance to a specific vector.

## Function syntax
The general function syntax for knn is: `distance(<target column>, <vector to compare with>, <metric> [, <weights>])`.

## KNN syntax
To express a k-Nearest-Neighbour search in SQL, you can combine the `distance` function with a `LIMIT` and `ORDER BY` clause.


## Examples

{% highlight sql %}
SELECT id, distance(arraycolumn, ARRAY[...], 'L2') as dist FROM tablewitharraycolumn ORDER BY dist ASC LIMIT 100;
SELECT id, distance(arraycolumn, ARRAY[...], 'L2', ARRAY[...]) as dist FROM tablewitharraycolumn ORDER BY dist ASC LIMIT 100;
{% endhighlight %}


## Supported metrics
Currently the following metrics are supported:
* L1
* L2
* L2 squared
* Cosine
* ChiSquared


