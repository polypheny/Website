---
title:  k-Nearest-Neighbor (KNN)
description: >
  How to use k-nearest-neighbour search in Polypheny.
hide_description: true
---

k-nearest-neighbour search functionality is a way to find entries based on their distance to a specific vector.

## Function syntax
The general function syntax for knn is: `knn(<target column>, <vector to compare with>, <metric> [, <weights>] [, <optimisation term>])`.

### Optimisation term
The optimisation term is useful for improving query performance.
It means that an underlying store may return only the `n` closest results (i.e. smallest metric).

The term does not guarantee that `n` results will be returned, a store can return more results (or less if there are less entries present).

## Examples

{% highlight sql %}
SELECT id, knn(arraycolumn, ARRAY[...], 'L2') FROM tablewitharraycolumn;
SELECT id, knn(arraycolumn, ARRAY[...], 'L2', ARRAY[...]) FROM tablewitharraycolumn;
SELECT id, knn(arraycolumn, ARRAY[...], 'L2', 100) FROM tablewitharraycolumn;
SELECT id, knn(arraycolumn, ARRAY[...], 'L2', ARRAY[...], 100) FROM tablewitharraycolumn;
{% endhighlight %}


## Supported metrics
Currently the following metrics are supported:
* L1
* L2
* L2 squared
* Cosine
* ChiSquared


