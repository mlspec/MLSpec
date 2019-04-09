# Machine Learning Pipeline
Machine learning pipelines are optimized around a data scientist's workflow and focus on making the model training process as efficient as possible.

## Graph

The core abstraction for Machine Leanring Pipelines is DAG, with every vertex being either 'data' or 'step' ('computation unit'), edges are data or control dependencies between verteces.

#### Vertices
'Data' vertex can be :
- [DataPath](../data/datapath.md)
- [DataSet](../data/dataset.md)

Data vertex has single output port.

'Step' vertex is always an instance of the [Module](module.md), with bound inputs, outputs and parameters. Module can be of two types: *primitive* (single script which can be executed on compute), and *complex* (subgraphs - DAGs themselves defined as above). This makes graph a nested recursive structure.

Step vertex can have many inputs (or none), and many outputs (or none).

#### Edges

There are two types of edges:
- Data dependency. Such edges connect data vertex or step output to input of another step. At execution time, input of that step will be set to specific instance of data

- Control dependency. Such edges connect step output to input of another step. This edge is not applicable to data verteces, and there is no data flow invloved. It purely represents that one step must be executed after another 

  Edges are always connecting inputs and outputs of vertices. Edges not associated with inputs and outputs are not allowed.

## Pipelines, Pipelines Drafts and Pipeline Runs

Graphs can be of two major classes: 
    - blueprint which defines what and how should be executed, and
        - particular executing instance
While both classes can look similarly, they are not exactly the same. Executing instance has naturaly properties like status, start time, logs, etc. Blueprint would insted define topology of the graph, parameter types and acceptable values, etc.

Mutable blueprint is called *Pipeline Draft*, and immutable preserved blueprint is called *Pipeline*. Executing instance is called *PipelineRun*

User can interactively construct a *Pipeline Draft*. This client side object defines DAG, and can be parametrized.  It is mutable during authoring, and then can be submitted for execution or published as *Pipeline* for future executions. When it's submitted for execution, *PipelineRun* is created and orchestrated by system. There are many ways to create *Pipeline Drafts* - *Pipeline Draft* can be defined by yaml file on disk, or in memory object in python, or created in UI interfaces, etc.

*Pipeline* is preserved immutable blueprint, which defines a parametrized DAG, and can be "instantiated" multiple times. Every time it's instantiated, it produces a PipelineRun which is then orchestrated by system.

*PipelineRun* is what is being executed by the system. While PipelineDraft or Pipeline graphs contain Steps, PipelineRun graph contains StepRuns - executing instances of Steps.

Mapping summary:

| Blueprint     | Executing Instance |
| ------------- | ------------------ |
| Step          | StepRun            |
| PipelineDraft | PipelineRun        |
| Pipeline      | PipelineRun        |

Transformation summary:

PipelineDraft.submit() -> PipelineRun

Pipeline.submit() -> PipelineRun
PipelineRun.clone() -> PipelineDraft
Pipline.clone() -> PipelineDraft

# Steps in a Pipeline
Step is always an instance of some [Module](module.md). Modules can be thought as reusable packages, and can be used many times in the same pipeline or in another pipelines. For convenience, we allow users to construct steps directly from scripts and binaries, but system is responsible to publish module and instantiate it in such cases.

#### Inputs and outputs

All data inputs and outputs are data stored in [DataStores](../data/datastore.md) . Single step can have inputs and outputs stored in different DataStores: both multiple data stores of the same type, and data stores of different types are allowed.

Step must have every non-optional input connected through edge to another vertex. Input can be connected only to single other vertex.

Step might have outputs **not** connected to other steps. Output can be connected to multiple other vertexes. Single output can be connected to multiple inputs of single vertex as well.

#### Parameters

Steps have all parameters set to specific values, either explicitly or implicitly (through default values defined for corresponding module)

## Parametrization

Pipeline Drafts and Pipelines can be parametrized with graph level parameters. Graph level parameters have names, types (string, float, etc.), default values and constrains defined. What PipelineRun is created from either Pipeline Draft or Pipeline, those parameters are set to actual values. Graph parameter names are unique within the graph.

## Pipeline Run

When graph is orchestrated, its execution is captured by *Pipeline Run*. 

Nodes in executing graph are *Pipeline Step Runs*. Each step run's output is a uniquely identified [Artifact](../data/artifact.md). When some step run finishes, and downstream step can be executed, orchestrator will ensure that corresponding artifacts are passed as inputs to the next step run.

Pipeline Run and each Step Run are runs - each having run id, logs, metrics and other metadata associated with them. See [Run](../experiment_tracking/run.md) for more details.

# A YML specification for a pipeline draft
See [pipeline.yml](pipeline.yml) for example
