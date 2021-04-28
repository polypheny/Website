---
layout: plain
title: Query File System (QFS)
---

The Query File System (QFS) data source adapter allows to map a directory including all its subdirectories as a relational table. This allows to query the content of a filesystem path. 

The mapped table contains the File itself as well as some of the file. The mapped table contains the following columns: 

| Column    | Description                                                                    |
|-----------|--------------------------------------------------------------------------------|
| path      | The absolute path of a file or directory.                                      |
| name      | The name of the file or directory.                                             |
| size      | The size of the file in bytes. Null if it is a directory.                      |
| file      | The file as a file object.                                                     | 

The check whether an entry represents a file, or a directory can easily be performed with a null check on the “size” column.

If the MultimediaFlavor is set to DEFAULT, the QFS source returns bytes instead of file references. If a row consists of a directory reference, the value of the “file” column is set to null. With the FILE MultimediaFlavor, the QFS source returns a file reference (pointing on a file or directory). The further handling depends on the query interface. The Polypheny-UI for instance allows to download the file (folders are being zipped automatically). 

The root path of the data source can be specified on deployment and can also be changed later. To prevent security issues, the QFS data source is working with a whitelist that consists of all allowed paths. The root directory must either be listed in the whitelist or needs to be a sub-directory of one of the entries in that whitelist. The whitelist is located in the config folder: `~/.polypheny/config/whitelist.config`
