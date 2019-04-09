# Dataset 

Datasets represent named data stored within a Datastore. Conceptually Datasets will be enabling data to be effectively used in various  scenarios by abstracting the underlying storage (such as formatting and encoding) and access complexities (such as reading and transforming to a meaningful form) 

# Dataset Version 

Datasets are versioned based on its definition (location of the data and steps to transform). Dataset definition can be simple Datapath (file path relative to Datastore) or a complex Dataflow (DataPrep dataflow json).  

Any changes to definition will necessitate the creation of a new version. Versioning concept is here same as source code commit in VSO or similar systems. 

# Archiving a Version 

Individual Dataset versions can be Archived when versions not supposed to be used for any reasons (such as underlying data no longer available). When an Archived Dataset version used in a Pipeline, execution will be blocked with error. No further actions can be performed on archived Dataset versions, but the references will be kept intact. 

# Deprecating a Version 

Individual Dataset versions can be deprecated when usage is no longer recommended and a replacement available. When a deprecated Dataset version used in a Pipeline, a warning message gets returned but execution will not be blocked.  

# Reactivate a Version 

Dataset versions can be reactivated to be used again. 

# Profile 

Profile of a Dataset version is Schema and various statistical measures of underlying data at a point in time. Profile of Dataset version will be stall when underlying data changes. 

Note: At this point only, Profile freshness can be calculated for file based Datastore (Azure Block Blob/ File Blob/ ADLS) 

# Dataset Checkpoint 

A checkpoint is a combination of Profile and an optional materialized copy of the data itself, tied to a specific dataset version. 

When data gets materialized, a new profile will be generated for the materialized data instead of current profile though it is still valid. This is to ensure freshness of the Profile while data being materialized.  

Also, when a checkpoint with materialized data is used in execution/ Training, the materialized data gets used instead of live data. 

# Dataset Views 

Dataset Views are simple user defined filters on a Dataset version to select subset of rows. Each Dataset View will have one Dataflow filter expression. Refer Dataflow expressions for more details. 

Eg: Weather Dataset version 1 can be pointing to all data between 2015 and 2018, The view will be Weather_2015, Weather_2016 and so on.
