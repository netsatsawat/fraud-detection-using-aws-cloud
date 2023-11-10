# Bring your own notebook to run on Amazon SageMaker Studio
---
This option is for those who wish to move and utilize the power of Cloud to run the machine learning model. This is **not** the recommended way of building the machine learning model using **Amazon SageMaker**.

<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/ec55b1e5d5908313787c146222e881afa70f1e5d/img/choose-instance.png" width=400>

## Why this is not recommended

If you are data scientist or model developer, you will usually spin up Jupyter Notebook or Python IDE to start exploring the data, creating feature engineering, building, optimising the models, and deploying it to the production within the same notebook. As such, you are most likely to spin up quite large amount of instances to support all those tasks in one notebook.

Amazon SageMaker allows data scientist to decouple the process by starting small instance (i.e., 2 vCPU, 4 GiB of RAM) to explore the data, and move all the other processes with each different instances, like; 
- Feature engineering move to [SageMaker Processing job](https://sagemaker-examples.readthedocs.io/en/latest/sagemaker_processing/index.html) or using [SageMaker Data Wrangler](https://aws.amazon.com/sagemaker/data-wrangler/)
- Build and train the model using [SageMaker Training job](https://docs.aws.amazon.com/sagemaker/latest/dg/how-it-works-training.html)
- Deploy the model using [SageMaker hosting](https://docs.aws.amazon.com/sagemaker/latest/dg/how-it-works-deployment.html)

Normally, model training and optimising are the most resource intensive task and requires a large instances (i.e., up to 64 vCPU or use multiple GPUs) depends on the workload of your model.

With this decoupling of data science process, data scientists can work more effective, innovate faster, and at the lower cost.
