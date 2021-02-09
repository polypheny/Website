---
layout: plain
title: Logging
description: >
  How to handle logging in Polypheny.
hide_description: true
---

This guideline describes how to handle logging in Polypheny.


## Log Levels

We use SLF4J as logging facade. Therefore, we have the following six log levels provided by SLF4J available:

1. trace (the least serious)
2. debug
3. info
4. warn
5. error
6. fatal (the most serious)


## Logger Annotation

We use Project Lombok for creating the logger field. It is therefore only required to add the `@Slf4j` Annotation to the class.

```java
@Slf4j
public class LogExample {
  
    public void foo() {
        log.error( "A sophisticated log message" );
    }
  
}
```


## Log Exceptions

The following code snippet shows how to log an exception:
 
```java
log.error( "An exception occurred!", new Exception( "Custom exception" ) );
```

Please do always log the whole exception object like showed above and do not call .getMessage() or similar. This ensures that the log output contains the stacktrace.


## Avoid string concatenation

Do not concatenate strings in logger calls. Use Use parameterized logger calls instead:

```java
log.info( "{} started and is listening on port {}.", name, getPort() );
```


## Guards

Use appropriate logging levels and make sure that there are "guards" in front of the lower levels. Use something like:

```java
if ( log.isTrace() ) {
    Info info = collectInformation();
	log.trace( "... {}", info.getSomething() );
}
```

This is especially important if additional method calls are required in order to prepare the log message. Furthermore, a guard avoids unnecessary concatenations and expression evaluations.

