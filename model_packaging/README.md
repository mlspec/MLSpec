# Model Packaging
Models may come from a variety of places:
-	Forked from a baseline experiment with sources tracked in a Git repository
-	Developed in a corporate environment's compliant experimentation system
-	Shared as part of a larger Model Ensemble.

Models may need to be consumed by several different upstream inferencing stacks. 
We should be able to track rich metadata around where models came from, what they are capable of, and where they are running.

# Why is this metadata important?
You are a bank being sued for discrimination in how you chose loan recipients via an ML model. 
Prove that the model you used was (a) not tampered with (b) had an audit trail for training and (c) the data set was unbiased.

# Key Requirements
- Track paper trail requirements for outputs produced in training pipelines.
-	Enable easy registration and updates of models across a variety of storage formats.
-	Provide a fluent command line experience / set of REST APIs for registering models.
-	Express model schema and service schema (how do I use the model?)
-	Support a model policy store
- Simplify operationalization of a model
-	Track model lineage
 -	Which code / data / experiment produced a model
 -	Pipelines used to produce a model 
 -	Other models used in the inference process for a model (composites)
- At minimum, capture the following:
 - 	code
 -	data
 - config (conda env, base docker image, … )
-	Track metrics associated with a model
 -	Make it easy to compare metrics across different versions of a model
-	Expose available deployment paths for inference
 -	What can we convert it to? Where can it be deployed to?
 -	New code or new model as a trigger for Deployment
 -	Change management integrated into the pipeline directly
-	Track breaking changes on models through semantic versioning
