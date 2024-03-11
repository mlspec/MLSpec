![MLSpec Logo](.//docs/assets/logos/mlspec_logo.png#gh-light-mode-only)
![MLSpec Logo](.//docs/assets/logos/mlspec_logo_light.png#gh-dark-mode-only)

**ML Spec is being revived with renewed interest and active development!**

ML Spec is an open-source framework for defining and verifying machine learning (ML) workflows.  The project aims to provide a standardized way to specify and validate the various stages of an ML pipeline, from data preprocessing to model training, evaluation, and deployment.

## Table of Contents

- [Project Status](#project-status)
  - [New Maintainer](#new-maintainer)
- [Background](#background)
  - [Foundational Work](#foundational-work)
  - [Existing Multi-Stage ML Workflows](#existing-multi-stage-ml-workflows)
- [Proposed Standards](#proposed-standards)
- [End-to-End Complete Lifecycle](#end-to-end-complete-lifecycle)
- [Repository Structure](#repository-structure)
- [Vision and Direction](#vision-and-direction)
- [Enhancing Model Interpretability and Trust](#enhancing-model-interpretability-and-trust)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Code of Conduct](#code-of-conduct)
- [Acknowledgments](#acknowledgments)
- [Help Shape The Future of ML Spec!](#help-shape-the-future-of-ml-spec)

## Project Status

After a period of inactivity, ML Spec is now under new maintainership and undergoing a revitalization effort. We are committed to breathing new life into this project, aligning it with the latest advancements in the ML ecosystem and addressing the evolving needs of the community.

### New Maintainer

M42 has taken over the maintainership of ML Spec and are excited to steer its future development. For any inquiries or suggestions, please feel free to reach out to me at av@messier42.com or @invariantly.

## Background

The field of machine learning has seen significant advancements in recent years, with the development of various frameworks, tools, and platforms to support the ML lifecycle. However, the lack of standardization and interoperability among these tools has led to challenges in reproducing, sharing, and governing ML workflows across different environments and organizations.

### Foundational Work

ML Spec builds upon the ideas and concepts from the foundational work in the field of ML workflow specification and verification. Some notable contributions include:

- [Predictive Model Markup Language (PMML)](https://en.wikipedia.org/wiki/Predictive_Model_Markup_Language)
- [Portable Format for Analytics (PFA)](https://dmg.org/pfa/)
- [ML Metadata](https://www.tensorflow.org/tfx/guide/mlmd)

These projects have paved the way for standardizing ML model serialization and metadata, but they primarily focus on individual models rather than end-to-end workflows.

ML Spec also draws inspiration from the MLSchema project, which has made significant contributions to the field of ML workflow specification. Due to the instability of the original MLSchema website, we have mirrored some of their key resources here:

- [MLSchema Paper](https://github.com/mlspec/MLSpec/blob/master/1807.05351.pdf)
- [MLSchema Core Specification](https://github.com/mlspec/MLSpec/blob/master/ML%20Schema%20Core%20Specification.pdf)

These resources provide valuable insights into the design principles and approaches behind ML workflow specification and have influenced the development of MLSpec.

### Existing Multi-Stage ML Workflows

In recent years, several prominent companies and organizations have developed their own multi-stage ML workflow solutions to address the challenges of managing end-to-end machine learning pipelines. These projects have focused on combining ML and batch processing capabilities to create robust and scalable workflows.

Some notable examples of these multi-stage ML workflow solutions include:

- [Facebook’s FBLearner Flow](https://code.fb.com/core-data/introducing-fblearner-flow-facebook-s-ai-backbone/): FBLearner Flow is Facebook's internal ML platform that enables engineers and data scientists to build, train, and deploy ML models at scale. It provides a unified interface for managing the entire ML lifecycle, from data preparation to model serving.

- [Google's TFX:](https://dl.acm.org/citation.cfm?id=3098021) TensorFlow Extended (TFX) is an end-to-end platform for deploying production ML pipelines. It provides a suite of components and libraries for building, training, and serving ML models, with a focus on scalability and reproducibility.

- [Kubeflow Pipelines](https://cloud.google.com/blog/products/ai-machine-learning/getting-started-kubeflow-pipelines): Kubeflow Pipelines is an open-source platform for building and deploying portable, scalable ML workflows on Kubernetes. It allows users to define and orchestrate complex ML pipelines using a declarative approach.

- [Microsoft Azure ML Pipelines](https://learn.microsoft.com/en-us/azure/machine-learning/concept-ml-pipelines?view=azureml-api-2): Azure ML Pipelines is a service within the Azure Machine Learning platform that enables the creation and management of end-to-end ML workflows. It provides a visual interface and SDK for building, scheduling, and monitoring ML pipelines.

- [Netflix Meson](https://netflixtechblog.com/meson-workflow-orchestration-for-netflix-recommendations-fc932625c1d9): Meson is Netflix's internal platform for building and managing ML workflows. It provides a unified framework for data preparation, model training, and deployment, with a focus on scalability and ease of use.

- [Spotify's Luigi](https://github.com/spotify/luigi): Luigi is an open-source Python library developed by Spotify for building and scheduling complex pipelines of batch jobs. While not specifically designed for ML workflows, it has been widely adopted in the ML community for managing data processing and model training pipelines.

- [Uber's Michelangelo](https://www.uber.com/blog/michelangelo-machine-learning-platform/): Michelangelo is Uber's ML platform that powers a wide range of services, from fraud detection to customer support. It provides end-to-end functionality for building, training, and deploying ML models at scale.

From studying these projects and their associated papers, we have identified a set of common steps that encompass the end-to-end machine learning workflow. These steps include data ingestion, data preparation, feature engineering, model training, model evaluation, model deployment, and monitoring.

ML Spec aims to provide a standardized specification and framework for defining and executing these multi-stage ML workflows, drawing inspiration from the successful approaches and best practices established by these industry leaders.

# Spec 

## Proposed Standards

ML Spec aims to establish a set of standards for various components involved in an end-to-end machine learning workflow. By defining these standards, ML Spec seeks to promote interoperability, reproducibility, and best practices across different ML tools and platforms.

The proposed standards cover the following key areas:

1. **Workflow Orchestration**: ML Spec will define a standard set of endpoints that each step in an ML workflow should expose. These endpoints may include:
   - `/ok`: An endpoint to check the health and readiness of the step.
   - `/varz`: An endpoint to retrieve various runtime variables and configurations.
   - `/metrics`: An endpoint to expose performance metrics and monitoring data.
   - Additional endpoints for step-specific functionality and control.

   By standardizing these endpoints, ML Spec enables consistent monitoring, control, and integration of ML workflow steps across different orchestration platforms.

2. **Model Management**: ML Spec will provide guidelines and standards for versioning, packaging, and deploying ML models. This may include:
   - Model serialization formats and conventions.
   - Metadata schemas for capturing model provenance, hyperparameters, and performance metrics.
   - APIs for model serving and inference.
   - Best practices for model versioning and lineage tracking.

   Standardizing model management practices promotes model reproducibility, interpretability, and maintainability.

3. **Logging**: ML Spec will define a standard logging format for capturing relevant information about each inference request. This logging format will align with the NCSA (National Center for Supercomputing Applications) standard log format, which includes fields such as:
   - Timestamp
   - Request ID
   - User ID
   - Model version
   - Input data
   - Output predictions
   - Latency
   - Additional metadata

   Adopting a standardized logging format enables consistent monitoring, debugging, and analysis of ML system behavior.

4. **Data Validation and Quality**: ML Spec will provide guidelines and standards for validating and ensuring the quality of input data at various stages of the ML workflow. This may include:
   - Data schema validation.
   - Data quality checks (e.g., missing values, outliers, data drift).
   - Data versioning and lineage tracking.
   - Integration with data validation frameworks and tools.

   Ensuring data quality and validation helps maintain the integrity and reliability of ML workflows.

5. **Experiment Tracking**: ML Spec will define standards for tracking and managing ML experiments, including:
   - Experiment metadata schemas.
   - APIs for logging and querying experiment runs.
   - Best practices for organizing and versioning experiment artifacts.
   - Integration with popular experiment tracking frameworks.

   Standardizing experiment tracking enables reproducibility, comparison, and analysis of ML experiments.

By establishing standards across these critical components of the ML workflow, ML Spec aims to foster a more robust, interoperable, and governed ecosystem for machine learning development and deployment.

## End-to-End Complete Lifecycle

With ML Spec, we believe that every stage of an ML lifecycle requires some form of metadata management. We have identified the following steps as critical components of a complete ML lifecycle:

1. **Codify Objectives**: Detail the model outputs, possible errors, and minimum success criteria for launching in code. Use a simple DSL that can be used to verify success/failure programmatically for automated deployment.

2. **Data Ingestion**: Specify the tools/connectors (e.g., ODBC, Spark, HDFS, CSV, etc.) used for pulling in data, along with the queries used (including signed datasets), sharding strategies, and any labeling or synthetic data generation/simulation techniques.

3. **Data Analysis**: Provide a set of descriptive statistics on the included features and configurable slices of the data. Identify outliers.

4. **Data Transformation**: Document the data conversions and feature wrangling techniques (e.g., feature to-integer mappings) used, as well as any outliers that were programmatically eliminated.

5. **Data Validation**: Apply validation to the data based on a versioned, succinct description of the expected properties of the data. Use schemas to prevent bad behavior, such as training on deprecated data. Provide mechanisms to generate the first version of the schema (e.g., `select * from foo limit 30`) that can be used to drive other platform components, such as automatic feature-engineering or data-analysis tools.

6. **Data Splitting (including partitioning)**: Record how the data is split into training, validation, hold back, and debugging sets, along with the results of validation for statistics of each set. Use metadata to detect leakage of training data into testing data and/or overfitting.

7. **Model Training/Tuning**: Capture metadata about how the model is packaged and the distribution strategy, hyperparameters searched and results of the search, results of any conversions to other model serving formats (e.g., TF -> ONNX), and techniques used to quantize/compress/prune the model and the results.

8. **Model Evaluation/Validation**: Record the results of evaluation and validation of models to ensure they meet the original codified objectives before serving them to users. Compute metrics on slices of data, both for improving performance and avoiding bias (e.g., gender A gets significantly better results than gender B). Document the source of data used for validation.

9. **Test**: Record the results of final confirmation for the model on the hold back data set. This MUST BE A SEPARATE STEP FROM #8. Document the source of data used for the final test.

10. **Model Packaging**: Capture metadata about the model package, including additional security constraints, monitoring agents, signing, etc. Provide descriptions of the necessary infrastructure (e.g., P100s, 16 GB of RAM, etc.).

11. **Serving**: Record the results of rolling the model out to production.

12. **Monitoring**: Provide live queryable metadata that enables liveness checking and ML-specific signals that need action, such as significant deviation from previous model performance or degradation of the model performance over time. Include a rollback strategy (e.g., if this model is failing, use `model last-year.last-month.pkl`).

13. **Logging**: Generate an NCSA-style record per inference request, including a cryptographically secure record of the version of the pipeline (including features) and data used to train.

By capturing and managing metadata at each stage of the ML lifecycle, ML Spec aims to provide a comprehensive and standardized approach to ensuring the reproducibility, interpretability, and governance of end-to-end machine learning workflows.

## Repository Structure

- [common](./common)

  - [object](./common/object.md)

    General notes applicable to multiple objects in the system. How they are identified and named, basic operations, etc.

- [data](./data)

  - [datastore](./data/datastore.md)

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

## Vision and Direction

Our vision for ML Spec is to establish it as a robust and widely adopted framework for defining, standardizing, and verifying complex ML workflows. We aim to:

1. **Enhance Framework Support**: Extend ML Spec to support the latest ML frameworks and libraries, such as PyTorch, XGBoost, and LightGBM, enabling seamless integration with cutting-edge techniques and architectures.

2. **Accommodate Complex Workflows**: Expand the ML Spec schema to accommodate intricate, multi-stage ML pipelines, including data preprocessing, feature engineering, model training, evaluation, and deployment.

3. **Integrate with MLOps and AutoML**: Align ML Spec with modern MLOps practices and AutoML frameworks, enabling streamlined workflow management and automation.

4. **Improve Governance and Compliance**: Introduce a methodology for recording attestations of workflow execution in accordance with schema to support governance and compliance requirements.

5. **Foster Community Engagement**: Revitalize the project's community by improving documentation, providing clear contributing guidelines, and actively engaging with users and contributors.

6. **Integrate with Workflow Orchestration Tools**: Provide seamless integration with popular workflow management platforms, such as Apache Airflow, Flyte, and Prefect, allowing users to leverage ML Spec for defining and verifying ML workflows within their existing orchestration pipelines.

## Enhancing Model Interpretability and Trust

One of the key challenges in the adoption and deployment of machine learning models is their interpretability and the trust users place in them. Many ML models are often considered "black boxes," making it difficult for users to understand how they arrive at their predictions or decisions. This lack of transparency can lead to a lack of trust and hesitation in relying on these models, especially in critical domains such as healthcare, finance, and legal systems.

MLSpec aims to address this challenge by providing a framework for building interpretable and transparent ML workflows. By standardizing the end-to-end ML lifecycle and promoting best practices for model development, evaluation, and deployment, MLSpec enables users to gain insights into the behavior and decision-making process of ML models.

Some of the ways MLSpec promotes model interpretability and trust include:

1. **Standardized Model Metadata**: MLSpec defines a standard schema for capturing and storing metadata about ML models, including information about their architecture, training data, hyperparameters, and performance metrics. This metadata provides a clear and comprehensive view of the model's characteristics and behavior.

2. **Model Evaluation and Validation**: MLSpec emphasizes rigorous model evaluation and validation practices to ensure that models meet the desired performance criteria and are free from biases or unintended consequences. By standardizing evaluation metrics and techniques, MLSpec enables users to assess the reliability and trustworthiness of models objectively.

3. **Model Explainability Techniques**: MLSpec encourages the use of model explainability techniques, such as feature importance analysis, partial dependence plots, and counterfactual explanations, to provide insights into how models make predictions. These techniques help users understand the factors influencing model decisions and identify potential issues or biases.

4. **Governance and Auditing**: MLSpec includes mechanisms for model governance and auditing, allowing organizations to track and monitor the lifecycle of ML models. This includes capturing information about model lineage, versioning, and approvals, ensuring that models adhere to regulatory requirements and ethical standards.

By focusing on model interpretability and trust, MLSpec aims to foster the responsible development and deployment of ML models. It provides the necessary tools and guidelines to build transparent and accountable ML workflows, enabling users to have confidence in the models they use and the decisions they make.

Join us in our mission to create a more interpretable and trustworthy ML ecosystem with MLSpec!

## Roadmap

Our short-term goals (next 3-6 months) include:

- [ ] Refactor the library codebase to improve maintainability and extensibility.
- [ ] Add support for PyTorch and XGBoost frameworks.
- [ ] Enhance the schema to accommodate complex, multi-stage workflows.
- [ ] Implement workflow attestation and digital signing capabilities.
- [ ] Overhaul the documentation and contributing guidelines.
- [ ] Develop an Apache Airflow operator/plugin for integrating ML Spec-defined workflows.

Our medium-term goals (6-12 months) include:

- [ ] Integrate with popular MLOps platforms and AutoML frameworks.
- [ ] Develop tools and dashboards for governance and compliance reporting.
- [ ] Collaborate with the Apache Airflow, Kubeflow, Prefect, Argo Workflows, MLflow, and Flyte communities to develop seamless integrations for defining and verifying ML workflows within their respective orchestration platforms.
- [ ] Establish industry partnerships and collaborations to promote adoption.
- [ ] Foster an active community of contributors and users.

We welcome contributions from the community to refine and expand this roadmap.

## Contributing

We are excited to have you on board! Please refer to the [CONTRIBUTING.md](CONTRIBUTING.md) file for detailed guidelines on how to get involved, whether it's by reporting issues, submitting pull requests, or participating in discussions.

## Code of Conduct

To ensure a welcoming and inclusive environment, we have adopted the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md). Please review and adhere to these guidelines.

## Acknowledgments

We would like to express our gratitude to David Aronchick (@aronchick) and the authors and contributors of ML Spec for their pioneering work on this project. Their efforts have laid the foundation for what we aim to achieve.

## Help Shape The Future of ML Spec!

We invite you to be a part of the ML Spec journey. Try out the new developments, provide feedback, and contribute your ideas and code. Together, we can shape the future of standardized and verifiable ML workflows.

For discussions and updates, stay tuned for upcoming mailing list and social accounts.

We believe ML Spec has the potential to become a foundational tool for building reliable and governed ML pipelines, and we look forward to working with the community to realize this vision.
