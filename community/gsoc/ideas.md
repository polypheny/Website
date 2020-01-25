---
layout: page
title: GSoC Project Ideas
---

Below, you can find some ideas on the directions in which we could push Polypheny together. Please consider them as starting points for your proposal. Of course, if you have other ideas, we would be very happy to hear them. Feel free to [contact us](/community/gsoc/#contact) and get feedback on what you plan to do beforehand.

* this unordered seed list will be replaced by toc as unordered list
{:toc}


## Query the blockchain
A blockchain can be seen as a distributed append-only database. The aim of this project is to build an adapter for executing (read) queries against (different) blockchains like the Bitcoin blockchain or the Ethereum blockchain.

**Difficulty**: medium-hard



## Quality check and assurance
A major problem in the process of developing any kind of software is to ensure that a change does not introduce any bugs in a completely different subsystem of the software.
For a database system this also includes to ensure the completeness and correctness of the results of a query.

Continuously and automatically checking that a system behaves and works like expected is therefore important to ensure consistent software quality and to avoid regressions. Usually, this is done using unit tests and integration tests. While unit tests check that individual parts (units) of the code (typically individual methods) work as expected, integration testing checks if the whole application works correctly.

Currently, Polypheny has only a few integration tests which make it hard to avoid regressions and unintended side effects. The aim of this project idea is to systematically add additional tests to cover as many features as possible. This especially means writing checks for the SQL query interface.

**Difficulty**: easy



##  Visualize it  
Visualization of planning and optimization decisions

**Difficulty**: medium-easy



## Support for Contextual Query Language

**Difficulty**: medium-hard



## RESTful query interface 

**Difficulty**: medium



## Predicting the future
Workload classification and forecasting

**Difficulty**: medium



## Keep them all     
A multi-version database system allows to store multiple versions of the same entry. This allows, for example, in a HR database to not only query the current salary of an employee, but also the salary he had two years ago.  

The goal of this project is to extend Polypheny-DB to transparently support storing multiple versions of an element including a full referential integrity for the past revisions. 

The project includes
* extending Polypheny's SQL dialect to support specifying a version,
* rewriting the queries to retrieve the right version and to add a new version if the query aims to modify an existing entry, and
* evaluate the correctness of the system especially for complex queries.

**Difficulty**: hard



## Physical query plan builder
The Polypheny-UI already comes with a logical query plan builder integrated. The aim of this project is to implement a graphical build tool for physical query plans similar to the one for logical query plans. In the polystore context, the physical query plan distinguishes from the logical one by using operators specific to the involved data store adapters. 

A physical query plan builder would be extremely helpful for development. Because there is already an implementation for logical plans, parts of the code can be reused. 

To get an impression how a physical query plan in Polypheny looks like you can simply execute a query in the UI and have a look at the plan by selecting "Physical Query Plan" in the left menu.

**Difficulty**: medium


