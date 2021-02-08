---
layout: plain
title: Project Structure
---

The Polypheny stack consists out of several parts. This page gives an overview about the different parts of the stack.


## Polypheny-DB
This is the main component of the Polypheny stack. Polypheny-DB is a self-adaptive polystore that provides cost- and workload aware access to heterogeneous data. As a polystore, Polypheny-DB seamlessly combines different underlying data storage engines to provide good query performance independent of the type of workload.


## Polypheny-UI
Polypheny UI is a powerful and easy to use web-based user interface for Polypheny-DB. The UI is deployed together with Polypheny-DB and can (by default) be accessed via port 8080.


## Polypheny Hub
Polypheny Hub is a platform for storing datasets and configurations.


## Polypheny Control 
Polypheny Control allows to easily deploy and monitor Polypheny-DB.


## Query-by-Gesture Bridge 
Middleware to connect Deepmime (gesture recognition) with Polypheny. It allows building and executing query plans by gestures.


## Polypheny Client 
Polypheny Client is a client for querying Polypheny-DB. It connects to Polypheny-DB via JDBC using the JDBC Driver. This client contains a [Chronos](https://github.com/chronos-eaas) connector. This allows to easily execute evaluation campaigns.


## Polypheny Simple Client 
A simple benchmarking and testing client for Polypheny. This client contains a [Chronos](https://github.com/chronos-eaas) connector. This allows to easily execute evaluation campaigns.


## Polypheny JDBC Driver 
A standards-compliant JDBC driver for Polypheny-DB.



