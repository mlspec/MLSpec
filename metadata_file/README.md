# [WIP] Metadata_file
This folder contains a metadata file for the ML job that we think what it should look like. We hope to recreate the ML job based on this metadata file. We started the first version of the metadata file based on Kubeflow mnist example, so we only focus on this one particular example. This metadata file will be expanded to adapt to more scenarios in ML world and we are happy to hear your advices.

Feel free to submit an issue or pr if you have any question or advice


# [WIP] Abstractions
There are 6 sections in the metadata description

1. *framework* - the name, version of the framework, also contains runtime and other supporting files for optional
2. *model* - the model used for this job
3. *dataset* - dataset acquisition, storage, loading and other dataset processings
4. *data_process* - different data process functions is applied based on different scenarios. Right now only some basic mnist image classification functions is included
5. *model_architecture* - includes input, output and other model architecture definitions
6. *training_params* - parameters for training, includes lr, loss, batch_size etc.


