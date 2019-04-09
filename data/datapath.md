# DataPath

### DataPath

DataPath is used to refer to something stored in DataStore. DataPath always contains reference to DataStore (which user usually does by name, and system usually tracks by Id), and DataStore type specific properties. In most cases it's relative path in given DataStore, but sometimes can be more complex, such as SQL Table name or SQL Query used to retrieve data from SQL Database.

Example DataPath:

```json
{
	"DataStore": "MyCloudStorageContainer",
	"RelativePath": "/data/summerproject/1.txt"
}
```

DataPaths don't have names, Ids, and other metadata. For those, see Artifacts and DataSets

