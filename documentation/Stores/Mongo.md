---
layout: plain
title: MongoDB Relational Adapter
---

## Deployment
The MongoDB adapter can be deployed with one of the following deployment methods:
- Remote
- Docker


## Adapter Settings

The adapter has the following settings when deployed:

| Setting              | Description                                                                                                                                                       |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| host (*remote only*)        | The name or IP address of the MongoDB instance.                                                                                                      |
| port                 | The port number of the deployed MongoDB instance.                                                                                                     |


## Relational Model
Polypheny-DB allows to store a relational model on a MongoDB store. To achieve this the relational model is mapped 
onto the underlying document model of the MongoDB instance. 
This allows the management of the relational model on the MongoDB store like every other relational store.
To enable this functionality, the following extensions to the MongoDB adapter are made through Polypheny:
- exclusive prepared statement logic 
- mapping of Polypheny-DB functions onto the MongoDB function interface

## Document Model (Comming Soon)


## Credits
- [MongoDB Java Driver](https://mongodb.github.io/mongo-java-driver/) Version 4.2.3
