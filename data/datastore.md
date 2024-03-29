# Datastore

### Datastore

Datastores are objects which indicate the location of a stored data. Example of Datastore can be a SQL Database, or cloud storage account like an Azure Blob or AWS S3 bucket, or DBFS file system in a Databricks cluster. Datastore can be either a pointer to the data, or used to store various pieces of data, organized into files, folders, sql tables, etc. - depending on its type.

The Datastore Object shouldn't be used for referencing specific file or folder, it's intended to be a bigger container. DataPaths are used to refer to specific data (like file or folder)  in Datastore. Datastore can be imagined as "place", and DataPath can be imagined as "thing" stored in "place".

Datastore has user assigned *name* and *type*, and system generated *id*. Depending on type, Datastore can have more properties. For example, for SQL Database can have properties such as connection string, database name.

Name is unique and assigned by user, at any moment of time only single datastore can have given name. User can rename Datastore. Id is also unique, but immutable and system generated. Usually *Id* is GUID.

Datastore can be archived. When it's archived, name is freed up and can be used for another Datastore.
