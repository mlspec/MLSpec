# Data tracking

Data tracking is built on several abstractions:

- [DataStore](datastore.md)

  A place for storing data. Could be a storage account, SQL database, HDFS filesystem, etc.

- [DataPath](datapath.md)

  A thing stored in DataStore. Always has reference to DataStore, and some way to specify location within it, for example relative path. Could be file, folder, table in SQL database, etc.

- [Artifact](artifact.md)

  Piece of data produced by run, has identifier (and can be stored in registry of artifacts) and DataPath.

- [DataSet](dataset.md)

  Named and versioned data, with rich metadata (profile, schema, snapshots, etc.). Uses DataPath to point to actual data.