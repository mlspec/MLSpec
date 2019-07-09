# MLSpec
A project to standardize the intercomponent schemas for a multi-stage ML Pipeline

# Background
The machine learning industry has embraced the concept of cloud-native architectures, made up of multiple component parts loosely coupled together. One of the issues with this approach, however, has been that while the steps of a machine learning pipeline have been fairly well articulated in a wide variety of publications, the specifications for how to wire together these steps remains highly varied, and make it difficult to build any standard tools that might simplify or formalize machine learning operations. 

This project is about establishing community driven standards that automated tooling can consume and output. Ideally, this enables the next opportunity around standardized ML software engineering practices. 

# Existing Multi-Stage ML Workflows
The below provide inspiration as projects which focus on ML and batch solutions:

- [Facebook’s FBLearner Flow](https://code.fb.com/core-data/introducing-fblearner-flow-facebook-s-ai-backbone/)
- [Google’s TFX Paper](https://dl.acm.org/citation.cfm?id=3098021)
- [Kubeflow Pipelines](https://cloud.google.com/blog/products/ai-machine-learning/getting-started-kubeflow-pipelines)
- [Microsoft Azure ML Pipelines](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-ml-pipelines)
- [Netflix Meson](https://medium.com/netflix-techblog/meson-workflow-orchestration-for-netflix-recommendations-fc932625c1d9)
- [Spotify’s Luigi](https://github.com/spotify/luigi)
- [Uber’s Michelangelo](https://eng.uber.com/michelangelo/) [[paper](http://proceedings.mlr.press/v67/li17a/li17a.pdf)]

From these papers, we feel the following steps summarize all the steps in an end-to-end machine learning workflow.

# Proposed standards
We propose a standard around the following components.

- Workflow orchestration – what are the standard endpoints that each step in an ML workflow require (e.g. /ok, /varz, /metrics, etc)
- Model - …
- Logging – what is the NCSA standard log for each inference request?
- Other…

# End-to-End Complete Lifecycle
We feel that over time, every stage of an ML lifecycle will need some form of metadata management. The below represent a collection of these steps:

1. *Codify Objectives* - Detail the model outputs, possible errors and minimum success for launching in code; a simple DSL that can be used to verify success/failure programmatically for automated deployment
2. *Data Ingestion* - What tools/connectors (e.g. ODBC, Spark, HDFS, CSV, etc) were used for pulling in data; what queries were used (including signed datasets); sharding strategies; May include labelling or synthetic data generation/simulation.
3. *Data Analysis* - Set of descriptive statistics on the included features and configurable slices of the data. Identification of outliers.
4. *Data Transformation* - What data conversions and feature wrangling (e.g. feature to-integer mappings) were used; what outliers were programmatically eliminated
5. *Data Validation* - What validation was applied to the data based on a versioned, succinct description of the expected properties of the data; schema can also be used to prevent bad behavior, such as training on deprecated data; mechanisms to  generate the first version of the schema (e.g. select * from foo limit 30) that can be used to drive other platform components, e.g., automatic feature-engineering or data-analysis tools.
6. *Data Splitting (including partitioning)* - How the data is split into training, validation, hold back & debugging sets and records and gets results of validation for statistics of each set; metadata here may be be used to detect leakage of training data into testing data and/or overfit
7. *Model Training/Tuning* - Metadata about how the model is packaged and the distribution strategy; hyperparameters searched and results of the search; results of any conversions to other model serving format (e.g. TF -> ONNX); techniques used to quantize/compress/prune model and the results  
8. *Model Evaluation/Validation*	- Result of evaluation and validation of model to ensure they meet original codified objectives before serving them to users; computation of metrics on slices of data, both for improving performance and avoiding bias (e.g. gender A gets significantly better results than gender B); source of data used for validation
9. *Test*	- Results of final confirmation for model on the hold back data set; MUST BE SEPARATE STEP FROM #8; source of data used for final test
10. *Model Packaging*	- Metadata about model package; includes adding additional security constraints, monitoring agents, signing, etc.; descriptions of the necessary infrastructure (e.g. P100s, 16 GB of RAM, etc)
11. *Serving*	- Results of rolling model out to production
12. *Monitoring* - Live queryable metadata that provides liveness checking and ML-specific signals that need action, such as significant deviation from previous model performance or degradation of the model performance over time; ideally includes rollback strategy (e.g. if this model is failing, use model last-year.last-month.pkl)
13. *Logging*	- NCSA-style record per inference request, including a cryptographically secure record of the version of the pipeline (including features) and data used to train.

# Table of contents for MLSpec repo

- [common](./common)

  - [object](./common/object.md)

    General notes applicable to multiple objects in the system. How they are identified and named, basic operations, etc.

- [data](./data)

  - [datastore](datastore.md)

    Data storages

  - [datapath](./data/datapath.md)

    Data references

  - [artifact](artifact.md)

    Data produced by runs

  - [dataset](./data/dataset.md)

    Named and versioned data in storage

- [pipelines](./pipelines)

  - [pipeline](pipeline.md)

    DAG for executing computation on data and training and deploying models

  - [module](module.md)

    Reusable definition of computation, includes script, set of expected inputs, outputs, etc.

- [experiment_tracking](./experiment_tracking)

  - [run](./experiment_tracking/run.md)

    Tracked execution of pipeline or single script on compute

- [model_packaging](./model_packaging)

  - [models](./model_packaging/README.md)

    Trained models

- logging_proto

- monitoring_proto

- [metadata_file](./metadata_file)

  - [metadata](./metadata_file/metadata.yaml)

    The metadata file used to recreate the ML workflow
