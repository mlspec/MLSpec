# Artifact

*Artifacts* are pieces of data produced by runs.

Artifacts have the following properties

- Id

  System assigned id, unique within workspace

- Name

  User assigned name, unique within the context of run which produced it

- Created By Run Id

  [Run](run.md) which produced this artifact

- Data Path

  Reference to data stored in storage (includes Data Store, relative path, etc.)

Artifact can be promoted to [DataSet](dataset.md)

