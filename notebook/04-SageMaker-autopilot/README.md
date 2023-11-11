# (Bonus) Using AutoML via SageMaker AutoPilot

Apart from creating model by your own by coding or using Amazon Fraud Detector, you can use **low-code/no-code** ML services namely **[Amazon SageMaker Canvas](https://aws.amazon.com/sagemaker/canvas/)** and **[Amazon SageMaker AutoPilot](https://docs.aws.amazon.com/sagemaker/latest/dg/autopilot-automate-model-development.html)**.

In this demonstration, I will use **SageMaker AutoPilot** module and calling them via **boto** SDK. 
You will need to only specify the target variable (column name), the S3 **input** and **output** location.

<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/601d1e10ac1ff6233925cf1fe3af094ec3a38e08/img/sm-autopilot-input-output-config.png" width=600>

And then call `create_auto_ml_job` or `create_auto_ml_job_v2` API. 

<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/601d1e10ac1ff6233925cf1fe3af094ec3a38e08/img/sm-autopilot-training-config.png" width=600>

That's it! You have already created the **AutoPilot** job. After the run, you can get best model candidate and deploy it to the endpoint. Or explore other model candidates created during the AutoPilot job. You can read more details in the notebook solution.

**Remark**: `CreateAutoMLJobV2` can manage tabular problem types identical to those of its previous version `CreateAutoMLJob`, as well as time-series forecasting, non-tabular problem types such as image or text classification, and text generation (LLMs fine-tuning).
