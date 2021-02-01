---
layout: page
title: PostgreSQL Adapter
---

The PostgreSQL adapter allows mapping existing tables on a remote PostgreSQL database into the schema of Polypheny-DB. One adapter can map multiple tables. This allows push-down of larger portions of a query. While the schema must be static and cannot be changed with Polypheny-DB, the data on the remote tables can be updated independently of Polypheny-DB. Polypheny-DB connects to the remote database system as a client and providing full support for transactions.


## Adapter Settings

The PostgreSQL adapter has the following settings: 

| Setting         | Description                                                                                                                                                       |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| host            | The name or IP adress of the remote PostgreSQL instance.                                                                                                          |
| port            | The JDBC port number of the remote PostgreSQL instance.                                                                                                           |
| database        | The name of the database containing the tables to be mapped.                                                                                                      |
| username        | The username to be used for authenticating at the remote PostgreSQL instance.                                                                                     |
| password        | The password to be used for authenticating at the remote PostgreSQL instance.                                                                                     |
| maxConnections  | The maximum number of concurrent JDBC connections.                                                                                                                |
| tables          | A list of tables which should be imported. The name must be in the format `schemaName.tableName`. Multiple names need to be separated by a comma.                 |


## Deployment

The adapter can either be deployed using the Polypheny-UI (Adapters -> Sources) or using the following SQL statement:

{% highlight sql %}
ALTER ADAPTERS ADD uniqueName 
   USING 'org.polypheny.db.adapter.jdbc.sources.PostgresqlSource' 
   WITH '{database:"postgres",host:"localhost",maxConnections:"25",password:"polypheny",username:"postgres",port:"5432",tables:"public.foo,public.bar"}'
{% endhighlight %}

Please make sure to adjust the settings according to your needs.

After the deployment, the specified tables are mapped into the public schema of Polypheny-DB. The tables and columns can be renamed. Furthermore, columns can be reordered and dropped (this is handled virtually; schema modifications are not forwarded to the remote database system). Dropped columns can be added again using the Polypheny-UI or the following SQL statement:

{% highlight sql %}
ALTER TABLE tableName ADD COLUMN physicalName AS name
{% endhighlight %}

`physicalName` thereby refers to the column name on the remote database system. 
