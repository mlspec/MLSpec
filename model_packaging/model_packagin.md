# Model Packaging Yaml file

The yaml file listed here allows to 'register' a model to a AI and ML platform. The goal is to define overall Model metadata in a standard way so that you can bring a model at any part of the lifecycle within the workflow system, if you so desire. For example someone might just want to train a model, or someone might have trained a model somewhere else, and would just like to serve. If they enter during training part, then some parts of the serving template should be filled automatically. Someone else might have a need to just convert their model to ONNX format and deploy. 

Even in serving, there will be different ways to describe your Model given how you have packaged them (container, or split pre-processing, prediction, post processing, and that too differs based on different model types). 

Training section is very evolved, and can handle multiple usecases. For serving, this starts with a sample for container based Model, but we hope to evolve in future.

 # General Model Metadata
 
```
 name: (Required) name of this model file
 description: (Optional) description of this model file 
 author: (Required for trainable)
   name: (Required for trainable) name of this training job's author
   email: (Required for trainable) email of this training job's author
 framework: (Required)
   name: (Required) ML/DL framework format that the model is stored as.
   version: (Optional) Framework version used for this model
   runtimes: (Required for trainable)
     name: (Required for trainable) programming language for the model runtime
     version: (Required for trainable) programming language version for the model runtime
 labels: (Optional list) labels and tags for this model
   - url: (Optional) Link to the ML/DL model page.
   - pipeline_uuids: (Optional) Linkage with a list of execuable pipelines.
 license: (Optional) License for this model.
 domain: (Optional) Domain metadata for this model.
 website:  (Optional) Links that explain this model in more details
```
# Data Required for Model Training

```
 train: (optional)
   trainable: (optional) Indicate the model is trainable. Default: False
   tested_platforms(optional list): platform on which this model can trained (current options: wml, ffdl, kubeflow)
   model_source: (Required for trainable)
     initial_model: (Required for trainable)
       data_store: (Required) datastore for the model code source
       bucket: (Required) Bucket that has the model code source
       path: (Required) Bucket path that has the model code source
       url: (Optional) Link to the model
     initial_model_local: (Optional)
       path: (Optional) Initial model code in the user local machine
   model_training_results: (Required for trainable)
     trained_model: (Required for trainable)
       data_store: (Required) datastore for the training result source
       bucket: (Required) Bucket that has the training result source
       path: (Required) Bucket path that has the training result source
       url: (Optional) Link to the model
     trained_model_local: (Optional)
       path: (Optional) Path to pull trained model in the user local machine
   data_source: (Optional)
     training_data: (Required for trainable)
       data_store: (Required) datastore for the model data source
       bucket: (Required) Bucket that has the model data source
       path: (Required) Bucket path that has the model data source
       url: (Optional) Link to the model
     training_data_local: (Optional)
       path: (Optional) Initial data files in the user local machine
   mount_type: (Required) object storage mount type
   evaluation_metrics: (optional) Define the metrics for the training job.
     type: (Required) evaluation_metrics type
     in: (Required) Path to store the evaluation_metrics
   training_container_image: (Optional)
     container_image_url: (Optional) Custom training container image url
     container_store: (Optional) container_store for the custom training image
   execution: (Required for trainable)
     command: (Required) Entrypoint commands to execute model code
       name: (Required) T-shirt size for training on Watson Machine Learning
       nodes: (Required) Number of nodes needed for this training job. Default: 1
   training_params: (Optional) list of hyperparameters for the training model
   	- (optional) list of key(param name):value(param value)
```

# Data required for Model Serving

```
 serve: (Optional)
   servable: (Optional) Indicate the model is servable without training. Default: False
   tested_platforms (optional list): platform on which this model can served (current options: kubernetes, knative, seldon, wml, kfserving)
   model_source: (Optional) - (Required if servable is true)
     servable_model: (Required for s3 or url type)
       data_store: (Required for s3 type) datastore for the model source
       bucket: (Required for s3 type) Bucket that has the model source
       path: (Required for s3 type) Source path to the model
       url: (Required for url type) Source URL for the model
     servable_model_local: (Optional)
       path: (Optional) Servable model path in the user local machine
   serving_container_image: (Required for container type)
     container_image_url: (Required for container type) Container image to serve the model.
     container_store: (Optional) container_store name
```

# Data Metedata 

```
 data (Optional)
   source_id: (Optional) Extension file id regarding the data source.
   domain: (Optional) Metadata about the data domain.
   website: (Optional) Links to the data description
   license: (Optional) Data license
```
 
 # Data Location 
 
 ```
 data_stores: (Optional) - (Required for trainable)
   - name: (Required) name of the data_stores
     connection:
       endpoing: (Required) Object Storage endpoint URL or public Object Storage key link.
       access_key_id: (Required) Object Storage access_key_id
       secret_access_key: (Required) Object secret_access_key
```

# Process - Mixin steps like training post process, serving pre process to be added

```
 process: (Optional)
     - name: (Required) Script Process name. Can mix any kind of process here
       params: (Optional) Free flowing list of key:value paisrs
        staging_dir: (Optional) Staging directory within the local machine
        trained_model_path: (Optional) trained model path within the object storage bucket
```

# Location for Docker container registry

```
container_stores: (Optional)
  - name: (Required) name of the container_store
    connection:
      container_registry: (Required) container registry for this container_store
      container_registry_token: (Required if container registry is private) container registry token
```

# Data required for Model conversion to ONNX format

```
 convert: (Optional)
   onnx_convertable: (Optional) Enable convertion to ONNX format.
                            The model needs to be either trainable or servable. Default: False
   model_source: (Required for onnx_convertable) Model binary path that needs the format conversion.
     data_store: (Required) datastore for the model source
     initial_model:
       bucket: (Required) Bucket that has the model source
       path: (Required) Bucket path that has the model source
       url: (Optional) Link to the model
     onnx_model:
       bucket:(Required) Bucket to store the onnx model
       path: (Required) Bucket path to store the onnx model
       url: (Optional) Link to the converted model
   tf_inputs: (Required for TensorFlow model) Input placeholder and shapes of the model.
   tf_outputs: (Required for TensorFlow model) Output placeholders of the model.
   tf_rtol: (Optional) Relative tolerance for TensorFlow
   tf_atol: (Optional) Absolute tolerance for TensorFlow
```
