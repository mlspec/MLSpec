# Inference Requests & Predictions
We will need to capture the following key attributes of an inference request to analyze drift & perform other upstream operations 
(such as labeling, feedback aggregation):

## Inference requests
- applicationId
- requestId # correlation ID
- requestTimestamp
- inputType
- inputFeatures (dictionary, string:string)
(for images, example features include dimensions, number of channels, dimension ordering, path to image file)
- groundTruthLabel

## Inference predictions
- applicationId
- requestId
- modelId (name/version)
- inferenceServiceId
- requestTimestamp
- inferenceLatency
- inputFeatures (dictionary, string:string)
- prediction
- predictionExplanation (dictionary, string:float) 
- predictionFeedback (float, 0:1, how useful was it)
- feedbackActions (list, string, what did the user do after the prediction came back)

Note that for ensemble cases (where requests are running through an inference pipeline) several of these may be generated. 
Do we log isFinal in ensemble case?
