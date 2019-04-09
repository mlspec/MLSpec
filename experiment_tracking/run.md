# Run

Run is a single execution of some 'job', such as script, pipeline, etc. Once executed, it can't execute again.

Runs have various metadata, metrics, artifacts, etc. associated with them. Also runs have references to other runs and other objects in the system

### Relationships

[TODO children/parent]

## Tags



## Metrics

## Artifacts

Artifacts are data produced by run. Single run can produce multiple artifacts. Artifacts are always stored as blobs identified by DataPaths - those could be files, folders, SQL tables, etc. Because Artifacts always point to data using DataPaths, they always represent data stored in DataStores. Different artifacts for given run can be stored in different DataStores. Some artifacts can be the published as (or promoted to) *DataSets*.

See [Artifact](artifact.md) for more information.

### Logs

Logs are represented as artifacts. Run can have several log objects - usual ones are stdout, stderr, driver log, etc. They are used to capture traces of executing job. Depending on implementation, logs can be raw text, or html or some other text.

