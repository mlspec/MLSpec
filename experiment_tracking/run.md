# Run

Run is a single execution of some 'job', such as script, pipeline, etc. Once executed, it can't execute again.

Runs have various metadata, metrics, artifacts, etc. associated with them. Also runs have references to other runs and other objects in the system

### Relationships

Runs can have parent-child relationships with other runs. These relationships help establish a hierarchical structure and capture dependencies between runs.

- Parent Run: A run can have a parent run, indicating that it is a part of a larger workflow or a subsequent run in a series of related runs. The parent run acts as a container or grouping mechanism for its child runs.
- Child Runs: A run can have multiple child runs, representing sub-tasks or sub-components of the parent run. Child runs are typically spawned by the parent run and can inherit certain properties or configurations from the parent.
The parent-child relationships can be captured using the following fields:

- parent_run_id: The ID of the parent run, if applicable. This field establishes the link between a child run and its parent run.
- child_run_ids: An array of IDs representing the child runs associated with the current run. This field allows for tracking the child runs spawned by the current run.
By capturing these relationships, you can create a hierarchical structure of runs, enabling better organization, traceability, and understanding of the dependencies between different parts of the ML workflow.

## Tags

Tags are key-value pairs that provide additional metadata and annotations for a run. They allow for flexible categorization, filtering, and querying of runs based on specific attributes or characteristics.

* Tags can be used to label runs with meaningful information, such as the purpose of the run, the algorithm used, the dataset version, or any other relevant contextual information.
* Each tag consists of a key and a value, both represented as strings.
* Multiple tags can be associated with a single run, allowing for rich metadata capture.
* Tags can be used to group related runs, filter runs based on specific criteria, or provide additional context for analysis and interpretation.

Example tags:

```
  - key: "experiment_type"
    value: "hyperparameter_tuning"
  - key: "dataset_version"
    value: "v2.0"
  - key: "algorithm"
    value: "random_forest"
```

## Metrics

Metrics are quantitative measurements or outcomes associated with a run. They capture the performance, accuracy, or other relevant numerical values that are recorded during the execution of a run.

* Metrics provide a way to track and compare the performance of different runs or experiments.
* Each metric consists of a key, which represents the name or identifier of the metric, and a value, which is the numerical value associated with the metric.
* Metrics can be of different types, such as scalar values (e.g., accuracy, loss), arrays or vectors (e.g., precision-recall curve), or even dictionaries or JSON objects for more complex metrics.
* Metrics can be captured at different points during the run, such as at regular intervals or at the end of the run.

Example metrics:

```
metrics:
  - key: "accuracy"
    value: 0.87
    value_type: "scalar"
  - key: "precision_recall_curve"
    value: [0.92, 0.88, 0.85, 0.80]
    value_type: "array"
  - key: "confusion_matrix"
    value: {
      "true_positive": 100,
      "true_negative": 200,
      "false_positive": 20,
      "false_negative": 30
    }
    value_type: "object"
```

## Artifacts

Artifacts are data produced by a run. A single run can produce multiple artifacts. Artifacts are always stored as blobs identified by DataPaths - those could be files, folders, SQL tables, etc. Because Artifacts always point to data using DataPaths, they always represent data stored in Datastores. Different artifacts for a given run can be stored in different Datastores. Some artifacts can be published as (or promoted to) DataSets.

See [Artifact](artifact.md) for more information.

### Logs

Logs are represented as artifacts. A run can have several log objects - usual ones are stdout, stderr, driver log, etc. They are used to capture traces of the executing job. Depending on the implementation, logs can be raw text, HTML, or some other text format.

