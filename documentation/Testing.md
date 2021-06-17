---
layout: plain
title: Testing
description: >
The used testsuites and how to include and exclude new tests correctly.
hide_description: true
---

## Testsuits
Polypheny-DB deploys 3 independent testsuites for testing different aspects of the polystore.
These are the following:
- Polypheny-DB Matrix
  This is the main testsuite, which executes all tests, as long as not specified otherwise. The 
- Polypheny-DB Docker CI
  This testsuite handles the Docker specific testing. To assign a new test to it the testclass has to be annotated with 
  the DockerManager category, like this:
```java
@Category(DockerManagerTest.class)
public class TestClass {
```

- Polypheny Adapter Matrix CI
  To provide an easy to adapt solution when working on new adapters or improving existing ones, 
  Polypheny-DB deploys this specific testsuite for thorough adapter testing.
  To include a new adapter in the testing suite automaticly one has to do following three steps:
  - Add the adapter-specific deployment settings to the class ```org.polypheny.db.catalog.Adapter```.
  - Generate a new class in core/src/test/java/org/polypheny/db/excluded/, 
    which is named with the following naming schema ```[name of your adapter]Excluded```.

### Exclude Tests
To exclude specific test methods, which your adapter does not support, annotate them with your adapter-specific ```[name of your adapter]Excluded``` class like this:
```java
@Category([name of your adapter]Excluded.class)
public void testingMethodYourAdapterDoesNotSupport(...
```
The same annoation can also be used to annotate full testclasses to exclude them for the new adapter.

```java
@Category([name of your adapter]Excluded.class)
public class TestClassWhichYourAdapterNotSupports {
```

  
  

