---
layout: plain
title: Project Structure
---

The Polypheny stack consists out of several parts. This page gives an overview about the different parts of the stack.


## Polypheny-DB
This is the main component of the Polypheny stack. 


## Polypheny-UI
Polypheny UI is a powerful and easy to use web-based user interface for Polypheny-DB. The UI is deployed together with Polypheny-DB and can (by default) be accessed via port 8080.


## Polypheny JDBC Driver 
Polypheny features a standards-compliant JDBC query interface. For accessing this interface we provide a corresponding JDBC Driver implementation. The driver also provides support for meta functions allowing to retrieve schema informations. 

The whole JDBC stack is implemented using _Avatica for Polypheny_ a fork of [Apache Avatica](https://calcite.apache.org/avatica/) containing Polypheny specific adjustments and extensions.


## Polypheny Control 
Polypheny Control is a tool for deploying and monitoring Polypheny. It takes care of pulling the required repositories and executing the builds. It comes with an easy to use browser-based user interface. This allows to setup, configure, build and monitor Polypheny in one, easy to use user interface.

In addition to the user interface, the whole functionality is also available through a REST-based interface. This allows to automatically perform even complex evaluation scenarios without any manual interaction.

In addition to the headless mode used for deploying Polypheny-DB on servers it also includes a mode for desktop systems. In this mode it starts a demon and adds itself to the taskbar. Polypheny Control is the recommended way for setting up Polypheny-DB.

In order to further simplify the setup, Polypheny Control contains an implementation of Git (using JGit) and Gradle. The only remaining system requirement is a Java JDK in version 8 or higher.


## Polypheny Hub
Polypheny Hub is a platform for storing datasets and schemas. While the frontend is integrated into Polypheny-UI, there is also a server application implemented in PHP which maintains and stores the actual datasets and schema definitions.

Importing and exporting datasets and schemas can conveniently be done directly within Polypheny-UI. Its also possible to do all management tasks like adding and removing users, setting user privileges, and managing datasets and schemas directly within Polypheny-UI.


## Polypheny Client 
Polypheny Client is a client for querying Polypheny-DB. It connects to Polypheny-DB via JDBC using the JDBC Driver. This client contains a [Chronos](https://chronos-eaas.org/) connector. This allows to easily execute evaluation campaigns.


## Polypheny Simple Client 
A simple benchmarking and testing client for Polypheny. This client contains a [Chronos](https://chronos-eaas.org/) connector. This allows to easily execute evaluation campaigns.


## Query-by-Gesture Bridge 
Polypheny-UI allows to build and execute logical query plans using a drag’n’drop based graphical builder. With Query-by-Gesture this builder can be controled using hand gestures. For recognizing the gestures it uses [Deepmime](https://deepmime.org/). The query-by-gesture plugin acts as a middleware between Polypheny-UI and Deepmime. 

