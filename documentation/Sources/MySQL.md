---
layout: page
title: MariaDB / MySQL Adapter
---

This adapter allows mapping existing tables on a remote MariaDB oder MySQL database into the schema of Polypheny-DB. One adapter can map multiple tables. This allows push-down of larger portions of a query. While the schema must be static and cannot be changed with Polypheny-DB, the data on the remote tables can be updated independently of Polypheny-DB. Polypheny-DB connects to the remote database system as a client and providing full support for transactions.


## Adapter Settings

The adapter has the following settings: 

| Setting              | Description                                                                                                                                                       |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| host                 | The name or IP address of the remote MariaDB or MySQL instance.                                                                                                   |
| port                 | The JDBC port number on the remote MariaDB or MySQL instance.                                                                                                     |
| database             | The name of the database containing the tables to be mapped.                                                                                                      |
| username             | The username to be used for authenticating at the remote MariaDB or MySQL instance.                                                                               |
| password             | The password to be used for authenticating at the remote MariaDB or MySQL instance.                                                                               |
| maxConnections       | The maximum number of concurrent JDBC connections.                                                                                                                |
| transactionIsolation | Which level of transaction isolation should be used. Available options: `SERIALIZABLE`, `READ_UNCOMMITTED`, `READ_COMMITTED`, `REPEATABLE_READ`                   |
| tables               | List of tables which should be imported. The names must to be separated by a comma.                                                                               |


## Deployment

The adapter can either be deployed using the Polypheny-UI (Adapters -> Sources) or using the following SQL statement:

{% highlight sql %}
ALTER ADAPTERS ADD uniqueName 
   USING 'org.polypheny.db.adapter.jdbc.sources.MysqlSource' 
   WITH '{database:"polypheny",host:"localhost",maxConnections:"25",password:"polypheny",username:"polypheny",port:"3306",transactionIsolation:"SERIALIZABLE",tables:"foo,bar"}'
{% endhighlight %}

Please make sure to adjust the settings according to your needs.

After the deployment, the specified tables are mapped into the public schema of Polypheny-DB. The tables and columns can be renamed. Furthermore, columns can be reordered and dropped (this is handled virtually; schema modifications are not forwarded to the remote database system). Dropped columns can be added again using the Polypheny-UI or the following SQL statement:

{% highlight sql %}
ALTER TABLE tableName ADD COLUMN physicalName AS name
{% endhighlight %}

`physicalName` thereby refers to the column name on the remote database system. 
